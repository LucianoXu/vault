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

The PARA component contains the `projects/`, `areas/`, `resources/`, `archive/` folders. In particular,
- `projects/` contains the ongoing works that have a clear deadline or target.
- `areas/` contains ongoing responsibilities with a standard to maintain (no end date), e.g. research, health, finances. 
- `resources/` contains the external materials that are helpful.
- `archive/` preserves the static projects or areas as they are. An archived entry keeps the
  internal structure it had while active and is not reorganized. Its folder takes a `YYYYMMDD_`
  prefix recording when it went inactive.

The Zettelkasten component is in `cards/`. `cards/` follows the structure of an *Obsidian* project, where markdowns with links forms the knowledge web. In our vault, we can also have links to the PARA contents.

- The Obsidian vault root is `assets/`.
- A card is named `YYYYMMDD Title.md`.
- Cards are categorized as fleeting or permanent, and labelled by YAML frontmatter (type: fleeting|permanent).
- Fleeting cards should be processed within 48h, either dropped or transformed into permanent cards.


## Credentials
Examples of credentials include login keywords, RSA key pairs, API keys, etc.


## Rules
- NEVER give away the credentials and sensitive information.
