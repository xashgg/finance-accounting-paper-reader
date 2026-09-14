# Finance and Accounting Paper Reader

A Codex skill for reading a single finance, accounting, or related academic paper through Zotero and producing an evidence-traceable Obsidian Markdown note.

## Reading modes

| Mode | Intended use | Approximate body length |
| --- | --- | --- |
| `quick` | Screening with compact source references | 800–1,500 words |
| `standard` (default) | Permanent literature note with selective Evidence Log | 2,000–3,500 words |
| `deep` | Detailed methodological and replication reading | No rigid limit |

All modes share the same typed YAML schema. The skill preserves important null and contrary findings, distinguishes prediction from causal identification, and protects manual notes.

## Requirements

- Codex with local skills support.
- A connected Zotero MCP integration providing read-only item metadata and paper retrieval capabilities. Tool availability is discovered at runtime.
- A verifiable Better BibTeX citation key for the output filename.
- An accessible Obsidian vault. Full text is preferred; incomplete coverage is labeled explicitly.
- An existing local YAML parser when available for frontmatter validation. The skill does not automatically install dependencies.

## Install

Download or clone this repository, then place its folder at `$CODEX_HOME/skills/finance-accounting-paper-reader`, or `~/.codex/skills/finance-accounting-paper-reader` when using the default Codex home. The installed folder must contain `SKILL.md`, `references/`, and `templates/` directly.

Supply your vault path in the reading request, or set `OBSIDIAN_VAULT_PATH` in the environment used to launch Codex. There is no hard-coded personal vault location. An explicit destination takes precedence over the environment variable.

Optionally copy `templates/Paper Note.md` to `<vault>/90_Templates/Paper Note.md` as the manual standard-mode fallback. Review any existing template before replacing it.

## Usage

```text
Use $finance-accounting-paper-reader to read <citekey> from Zotero.
Save the note in <vault>/10_Papers/<citekey>.md. Do not overwrite an existing note.
```

```text
Use $finance-accounting-paper-reader in quick mode to read <citekey>.
```

```text
Use $finance-accounting-paper-reader in deep mode to read <citekey>.
```

Replace angle-bracket placeholders with actual values. If no mode is specified, the skill uses `standard`. If no vault is configured, it asks for the location before saving.

## Repository structure

```text
SKILL.md                           Operational workflow and mode selection
references/paper-note-template.md  Shared YAML schema and mode-specific bodies
references/field-guidelines.md     Finance/accounting methodological guidance
templates/Paper Note.md            Manual standard-mode Obsidian template
```

Keep the manual template aligned with the shared schema and standard body when changing the skill. Existing paper notes are not migration targets and should not be committed to this repository. Do not commit personal vault paths, Zotero libraries, credentials, or copyrighted PDFs.

## License

No license has been selected. Add a license before distributing this project under open-source terms.
