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

### Names must be legal on every replica

The Vault replicates to Windows (NTFS), so a name is only valid if Windows accepts it.
The Unix replicas accept far more than NTFS does, which makes this failure silent from macOS or
Linux: the entry syncs cleanly between the Unix replicas, then fails **forever** on Windows with
`syncing: name is invalid, contains Windows reserved character`. The file never lands there and
the folder never reaches a clean state. Nothing warns you at creation time.

- **Never use** `< > : " / \ | ? *` or control characters anywhere in a name. `:` and `|` are the
  ones that slip in most often — from timestamps, and from web page titles saved to disk.
- **No trailing space or trailing dot.** Windows silently strips both, so `Draft ` and `Draft`
  collide.
- **Avoid the reserved device names** `CON`, `PRN`, `AUX`, `NUL`, `COM0`-`COM9`, `LPT0`-`LPT9`.
  They are reserved with any extension too: `NUL.md` is as unusable as `NUL`.
- **Case alone never distinguishes two entries.** Both macOS and Windows are case-insensitive, so
  `Notes.md` and `notes.md` cannot coexist in one directory — only Linux would keep them apart.
- **Never name anything in the shape `NAME~N.EXT`** (`PAGE_2~4.JPG`, `REPORT~1.DOC`). NTFS
  auto-generates exactly that shape as the hidden 8.3 short name of every long filename, and it
  refuses to create a real file whose name collides with a sibling's generated short name. The
  failure is invisible in advance — which sibling gets which alias depends on directory order —
  and it surfaces on Windows as `syncing: finishing: replacing file: file does not exist`, with the
  content fully downloaded and stuck in a `~syncthing~*.tmp`. Such names usually arrive from old
  FAT-era transfers; rename them on import. `dir /x` on Windows lists the generated short names.
- The 100-character ceiling above is partly this rule: deep nesting plus long names runs into
  Windows path limits, and the limit applies to the whole path, not the single name.

When importing anything named by an external tool — a saved web page, an export, a scanned batch —
rename it on the way in. That is what `inbox/` processing is for.


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
- Folders starting with `stignore-*` are not synchronized. This can be used as machine-specific folders, such as build output.
