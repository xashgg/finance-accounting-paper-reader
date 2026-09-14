# Finance and Accounting Paper Reader

A Codex skill that reads one finance, accounting, or related academic paper from Zotero and creates an evidence-traceable Markdown literature note for Obsidian.

The skill matches the intended Zotero record, verifies the Better BibTeX citation key, reads the available paper text, and writes the note to:

```text
<vault>/10_Papers/<citekey>.md
```

It is designed for permanent research notes rather than generic paper summaries. Claims are tied to verified source locations, important null or contrary results are retained, and incomplete full-text coverage is disclosed.

## Features

- Matches papers by Better BibTeX citekey, Zotero item key, DOI, title, or author and year.
- Keeps bibliographic parent keys separate from attachment keys.
- Supports `quick`, `standard`, and `deep` reading modes.
- Uses one typed YAML schema across all modes for compatibility with Obsidian Bases.
- Distinguishes paper type, research design, methods, and causal identification.
- Records a defensible primary analysis sample size without cataloguing every regression sample.
- Preserves signs, statistical significance, economic magnitude, and material null or contrary findings.
- Scales source traceability from compact inline citations to a comprehensive Evidence Log.
- Labels partial or unavailable full text instead of filling gaps with unsupported claims.
- Protects user-authored content when updating an existing note.
- Validates YAML frontmatter with an available local parser when feasible.

## Reading modes

| Mode | Use case | Typical body length | Evidence detail |
| --- | --- | ---: | --- |
| `quick` | Screen a paper for relevance | 800–1,500 words | Compact source locations for central claims |
| `standard` | Create a routine permanent literature note | 2,000–3,500 words | Selective Evidence Log, usually 5–12 entries |
| `deep` | Study a cornerstone paper, method, or replication target | No fixed limit | Detailed design, exhibits, appendices, and replication concerns |

`standard` is used automatically when no mode is specified. Reading mode controls synthesis depth; it does not relax evidence or source-verification requirements.

## Requirements

- Codex with local skill support.
- Zotero Desktop and a compatible Zotero MCP connection with read access to the library.
- Better BibTeX when citekey-based filenames are required.
- An accessible Obsidian vault.
- Usable paper full text for a complete reading note. Metadata-only and partial notes are supported and labeled accordingly.

The skill discovers the Zotero tools available in the current environment. It does not modify Zotero items, annotations, tags, settings, or indexes.

## Installation

Clone or download this repository into the Codex skills directory:

```text
$CODEX_HOME/skills/finance-accounting-paper-reader
```

If `CODEX_HOME` is not set, use the default location:

```text
~/.codex/skills/finance-accounting-paper-reader
```

The installed directory should have this shape:

```text
finance-accounting-paper-reader/
├── .env.example
├── SKILL.md
├── references/
│   ├── field-guidelines.md
│   └── paper-note-template.md
└── templates/
    └── Paper Note.md
```

Restart Codex or begin a new session if the skill does not appear immediately after installation.

## Vault configuration

The easiest persistent setup is a local `.env` file in the installed skill directory. Copy `.env.example` to `.env` and replace the placeholder with the absolute path to your vault:

```dotenv
OBSIDIAN_VAULT_PATH=/absolute/path/to/your/Obsidian/vault
```

The skill reads this file automatically, so the vault path does not need to be repeated in every request. The local `.env` file is ignored by Git and should remain uncommitted.

You can instead define `OBSIDIAN_VAULT_PATH` in the environment used to launch Codex:

PowerShell:

```powershell
$env:OBSIDIAN_VAULT_PATH = "C:\path\to\your\vault"
```

macOS or Linux:

```bash
export OBSIDIAN_VAULT_PATH="/path/to/your/vault"
```

Vault resolution follows this order:

1. An explicit destination in the current request
2. An established value in the current session
3. The process-level `OBSIDIAN_VAULT_PATH`
4. `OBSIDIAN_VAULT_PATH` in the skill directory's `.env`

The skill treats `.env` as plain configuration data and does not execute it. The tracked repository contains only `.env.example`, with no personal vault path.

The optional manual template can be copied from [`templates/Paper Note.md`](templates/Paper%20Note.md) to:

```text
<vault>/90_Templates/Paper Note.md
```

Review an existing vault template before replacing it. The bundled template represents `standard` mode; the skill selects the appropriate body for other modes.

## Usage

Standard mode with a Better BibTeX citekey:

```text
Use $finance-accounting-paper-reader to read smith2025EarningsQuality from Zotero.
Do not overwrite an existing note.
```

Quick screening:

```text
Use $finance-accounting-paper-reader in quick mode to read
smith2025EarningsQuality from Zotero.
```

Deep reading:

```text
Use $finance-accounting-paper-reader in deep mode to read
smith2025EarningsQuality from Zotero.
```

Explicit vault destination:

```text
Use $finance-accounting-paper-reader to read smith2025EarningsQuality.
Save the note to C:/path/to/vault/10_Papers/<citekey>.md.
Do not overwrite any existing note.
```

The paper may also be identified by Zotero item key, DOI, exact title, or author and year. The skill still requires a verified Better BibTeX citekey before creating a citekey-named file.

## Output

Every reading mode uses the same YAML properties and types. The schema includes bibliographic identity, Zotero identity, topics and theories, paper type, research design, methods, identification strategy, data sources, sample metadata, reading mode, reading status, and full-text status.

The Markdown body changes by reading mode. A standard empirical-paper note covers:

1. One-Sentence Takeaway
2. Research Question and Gap
3. Contribution
4. Theory
5. Data and Sample
6. Variable Construction
7. Research Design and Identification
8. Main Results
9. Mechanism and Heterogeneity
10. Robustness
11. Position in Literature
12. Evidence Log
13. Replication Resources
14. Citation-Ready Summary
15. A protected `My Notes` region

The structure adapts to predictive, experimental, analytical, structural, qualitative, review, and other paper types while retaining the relevant core analytical roles.

## Existing-note safety

New notes contain separate generated-content and user-notes markers. When a destination already exists, the skill reads it before proposing an update and preserves identifiable user-authored material, unknown YAML fields, ratings, projects, and manual notes. If generated and manual content cannot be separated safely, the existing file is left unchanged and the conflict is reported.

The skill does not bulk-migrate a vault, rename legacy notes, or rewrite the manual Obsidian template during routine paper reading.

## Repository structure

| Path | Responsibility |
| --- | --- |
| [`.env.example`](.env.example) | Sanitized example for persistent local vault configuration |
| [`SKILL.md`](SKILL.md) | Operational workflow, reading-mode selection, source discipline, safe updates, and quality control |
| [`references/paper-note-template.md`](references/paper-note-template.md) | Shared YAML schema and mode-specific note structures |
| [`references/field-guidelines.md`](references/field-guidelines.md) | Finance/accounting methodological reading guidance |
| [`templates/Paper Note.md`](templates/Paper%20Note.md) | Manual Obsidian fallback aligned with standard mode |

When changing the output schema, update the reference template and the manual Obsidian template together. Existing notes are backward-compatible records and are not automatic migration targets.

## Privacy and repository hygiene

Do not commit personal vault paths, Zotero database files, exported libraries, credentials, copyrighted PDFs, or generated research notes. The included `.gitignore` excludes `.env` and common local research data. Confirm the rule with `git check-ignore .env` after setup and still review changes before each commit.

## Validation

After changing the skill, run the validator bundled with Codex's `skill-creator` skill:

```text
python <skill-creator>/scripts/quick_validate.py <path-to-this-repository>
```

Also verify that the YAML schema in `references/paper-note-template.md` matches the frontmatter in `templates/Paper Note.md` and that the manual template matches the standard-mode body.

## License

No license has been selected. Add an appropriate license before distributing the repository under open-source terms.
