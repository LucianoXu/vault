# The Vault System

This file describes the design, structure and operations of the Vault system. 
The Vault system works as the digital database and control center for the user. The user identity is preserved in `USER.md`.

The Vault system supports distributed storage and computation. 
`infrastructure/` contains textual descriptions of the external entities the user holds but whose content the Vault does not own — machines, storage, domains, cloud accounts — each as a file.
We say the Vault system **owns** an asset if the asset content is located directly in the folder. The Vault can also **record** a reference to the asset, which is a markdown file describing the content and its location.

The entire vault will be synchronized by *Syncthing*. The Vault system skeleton itself is tracked by *Git*.
The Vault system is expected to be operated by both human and AI. 
The assets are in `assets/`. Its organization combines the PARA framework by Tiago Forte and the Zettelkasten method.
The credentials of the user are in `credentials/`.
`templates/` holds the skeletons for instance files.


## I/O Guideline

The `inbox/` and `outbox/` folders serve as the official UI I/O endpoints.
Contents in `inbox/` are processed periodically (at least every week), renamed properly, and integrated into the Vault according to its content.
Ask the user before dropping input contents.
Assets that explicitly required by the user should be copied to or refered to `outbox/`, which is cleaned periodically.


## Assets

The PARA component organizes actual projects, codebase and materials, while the Zettelkasten component work as a textual knowledge web that connects different ideas.

The PARA component contains the `1-projects/`, `2-areas/`, `3-resources/`, `4-archive/` folders. In particular,
- `1-projects/` contains the ongoing works that have a clear deadline or target.
- `2-areas/` contains ongoing responsibilities with a standard to maintain (no end date), e.g. research, health, finances. 
- `3-resources/` contains the static materials that are helpful.
- `4-archive/` preserves the static projects or areas as they are. An archived entry keeps the
  internal structure it had while active and is not reorganized. Its folder takes a `YYYYMMDD_`
  prefix recording when it went inactive.

The Zettelkasten component is in `0-cards/`. `0-cards/` follows the structure of an *Obsidian* project, where markdowns with links form the knowledge web. Our vault is not constrained by Obsidian functionality and we can also have links to other contents outside `0-cards/`.

- A card is named `YYYYMMDD Title.md` (creation date).
- Cards are categorized as fleeting or permanent, and labelled by YAML frontmatter (type: fleeting|permanent).
- Fleeting cards should be processed within 48h, either dropped or transformed into permanent cards.


## Naming

A name is an identifier before it is a label: it must say what the entry holds, so the entry
can be found without being opened.

- **English names use PascalCase** — no spaces, hyphens or underscores. Acronyms and brand names keep their own capitalisation.
- **Chinese names stay in Chinese** and take no case convention.
- Names must survive nesting: stay under 60 characters, never exceed 100.


## Synchronization

- **Pause the folder before any bulk rename or move.** Under a live watcher every file becomes its
  own index event. Pause, change, rescan once, resume.
- **A case-only rename needs an intermediate step.** macOS is case-insensitive.
- **Local status does not report remote health.** A device sits at `idle` with no errors while a
  replica retries the same pull forever. Check `db/completion` per device, not folder state.


## Credentials
Examples of credentials include login keywords, RSA key pairs, API keys, etc.


## Rules
- NEVER give away the credentials and sensitive information.
