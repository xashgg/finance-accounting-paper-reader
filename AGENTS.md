# Project guidance

This repository defines the `finance-accounting-paper-reader` Codex skill. Keep the
skill instructions, reference schema, manual Obsidian template, and bilingual user
documentation aligned.

## Sources of truth

- `SKILL.md` defines the operational workflow and safety rules.
- `references/paper-note-template.md` defines the canonical YAML schema and the
  `quick`, `standard`, and `deep` note bodies.
- `references/field-guidelines.md` defines the finance/accounting extraction checks.
- `templates/Paper Note.md` is the manual fallback for the standard-mode note.
- `README.md` and `README.zh-CN.md` are parallel user-facing documentation.

## Maintenance rules

- When changing the YAML schema, update the canonical reference and manual template
  together. Preserve every schema property and its type across all reading modes.
- When changing the standard body, keep the corresponding block in
  `references/paper-note-template.md` and `templates/Paper Note.md` identical.
- Keep the English and Chinese READMEs equivalent in features, setup, usage, safety,
  repository structure, and validation guidance.
- Never commit personal vault paths, credentials, Zotero databases, copyrighted PDFs,
  exported libraries, or generated research notes.
- Do not migrate or rewrite existing vault notes merely because this skill changes.

## Validation

After changes, run the validator bundled with Codex's `skill-creator` skill, then
verify local Markdown links, frontmatter parity, standard-body parity, and
`git check-ignore .env`.
