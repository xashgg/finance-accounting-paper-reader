---
name: finance-accounting-paper-reader
description: Read an individual finance, accounting, or related academic paper via Zotero MCP and create or safely update an evidence-traceable Markdown research note in Obsidian. Use with a Better BibTeX citation key, Zotero item key, DOI, title, or author and year when the user requests paper reading or a paper note.
---

# Finance and Accounting Paper Reader

Create a rigorous note for one identified paper. Resolve the vault from the user's explicit destination or established session configuration, then `OBSIDIAN_VAULT_PATH` if set. If no vault is configured, ask for its location before saving; reading and analysis may proceed independently. Canonical output: `<vault>/10_Papers/<citekey>.md`. Resolve paths for the host operating system. Never guess a personal folder path or substitute a similarly named vault silently.

Read [references/paper-note-template.md](references/paper-note-template.md) for the authoritative output schema. Read the core and applicable design/type sections of [references/field-guidelines.md](references/field-guidelines.md) before analysis. The first reference defines the note; the second defines what to extract and assess.

## Select reading mode

Use `standard` when no mode is specified; do not ask. Recognize natural requests such as "in quick mode" or "in deep mode". Record the selected mode in `reading_mode`; it controls synthesis depth, not permission to lower evidence standards.

| Mode | Purpose | Body length guidance | Evidence treatment |
|---|---|---|---|
| quick | Rapid screening for further reading | About 800-1,500 words, excluding YAML | Compact inline locations for central claims; no full Evidence Log or routine table reconstruction |
| standard | Routine serious reading and a permanent literature note; default | About 2,000-3,500 words for a typical empirical paper; somewhat more for complexity | Selective Evidence Log, usually 5-12 entries: sample, focal variables, design, main findings, major mechanism/robustness results |
| deep | Cornerstone, method adoption, replication-oriented, referee-style or project-critical reading | No rigid limit | Comprehensive evidence, applicable design details, exhibit mapping, substantive inconsistencies and appendix coverage |

All modes use the identical YAML schema and property types defined in the reference. Never drop properties for quick mode; use null/empty arrays for unverified information. Use the mode's body structure from the reference. Length targets do not justify padding sparse evidence, omitting important contrary findings, or truncating necessary qualifications.

## Identify the paper through Zotero MCP

Discover the currently exposed tool schemas; do not assume every deployment has identical capabilities. Use read-only Zotero operations. Do not add items, annotations, notes, tags, update the database/search index, change Better BibTeX settings, or enable/restart services as part of reading.

Prefer matching in this order, using only identifiers actually supplied or verified:

1. Exact, case-sensitive Better BibTeX citation key.
2. Zotero item key (resolve an attachment or note to its bibliographic parent).
3. DOI, normalized by removing a DOI URL or `doi:` prefix and comparing without case sensitivity.
4. Exact title, allowing formatting/whitespace normalization but no substantive title substitution.
5. Author and year, corroborated with title, coauthors, venue, and version.

Known read-only capabilities are listed below (names omit the MCP namespace). Discover the actual schemas before using them; this table is a routing aid, not a guarantee of identical deployment behavior.

| Purpose | Tool and usage |
|---|---|
| Exact Better BibTeX lookup | `zotero_search_by_citation_key(citekey=...)` |
| Complete item metadata | `zotero_get_item_metadata(item_key=..., format="json")` |
| Candidate discovery | `zotero_search_items(query=..., qmode="titleCreatorYear")`; use short title/author queries |
| Structured filtering | `zotero_advanced_search(conditions=[...], join_mode="all")`; use only supported fields/operations |
| Attachments and appendices | `zotero_get_item_children(item_key=...)` |
| Main attachment text | `zotero_get_item_fulltext(item_key=...)`, using the parent key |
| PDF orientation | `zotero_get_pdf_outline(item_key=...)`, selected attachment key, or bibliographic parent if required by the deployment |
| Page-by-page reading | `zotero_read_pdf_pages(item_key=..., start_page=..., end_page=...)`; PDF pages are 1-indexed |
| Local attachment fallback | `zotero_get_attachment_path(item_key=...)`, when available in local mode |
| Library discovery | `zotero_list_libraries()`, only when library scope needs resolution |

Search output may use simplified queries or semantic fallback: its rank is not proof of identity. Inspect candidate records. If DOI filtering is unsupported, discover candidates from accompanying title/author metadata or a primary DOI page, then compare their actual DOI fields. Do not send a DOI to an item-key parameter.

Report ambiguous candidates with citation key, item key, title, authors, year, and DOI; ask the user to select when evidence cannot distinguish them. Do not silently choose a duplicate record, working paper versus published version, or a result from the wrong library. A Zotero key is persistent within its library; retain returned library identity/URI as well when available.

Preserve both the citation key (human-facing identifier) and bibliographic parent item key (machine identifier); keep attachment keys separate from the parent key in working source tracking. Include them in the permanent note only when they materially clarify source identity. Recover the assigned Better BibTeX key from verified lookup or explicit returned citation-key metadata. Generic BibTeX exports may generate a different key: do not assume an export key is the Better BibTeX key. If necessary, inspect a supported read-only Better BibTeX retrieval capability. Never synthesize a key from author/year/title. Without a verified key, report the filename blocker and provide analysis in the conversation if useful; do not save a title- or item-key-named substitute.

## Retrieve and read the full paper

Retrieve complete metadata, enumerate attachments, and identify the paper version and relevant online/Internet appendices. In standard and deep modes, read the full main paper, including tables, figures, footnotes, and in-paper appendices. Quick mode also reads the full paper when readily available, then summarizes selectively. If complete text cannot be obtained, continue with an honestly labeled incomplete note rather than inventing analysis. Retrieve relevant separate appendices for claims that depend on them; deep mode additionally maps available supplementary coverage.

A tool named "fulltext" does not establish completeness: extraction can be page-limited, truncated, unindexed, or empty for scanned PDFs. Use the outline and document page count where available; maintain a working coverage record of sections/pages read and gaps while analyzing the paper. Complete missing ranges with page-reading tools or the returned local PDF path. Inspect rendered pages where equations, table alignment, minus signs, significance marks, or figures are ambiguous or material to the retained claims. Use existing OCR/PDF capabilities where necessary; report unavailable capabilities instead of installing dependencies automatically.

If Zotero has no usable full text, try accessible primary sources via DOI/publisher, official author or institutional repositories, and supplied local files. Verify that the downloaded version matches the identified paper. Do not combine working-paper results with published-paper metadata without an explicit version qualification. Metadata, abstracts, Zotero notes, and secondary summaries do not replace the paper.

Set coverage independently of requested mode:

- `full_text_status: available` only after the full main paper has been read. Use `status: read` for completed quick/standard notes and `status: deep-read` for completed deep notes.
- `full_text_status: partial` and `status: partial-read` for incomplete reading or material extraction gaps, even when deep mode was requested.
- `full_text_status: unavailable` and `status: metadata-only` when no usable full text was obtained.

Report coverage and separate-appendix availability in the final delivery. Follow the reference's optional, compact Reading Record policy. Keep substantive version or coverage issues in the note; exclude routine MCP failures, attachment-path debugging, HTTP errors, token/display limits, extraction implementation details, copyright-page details and temporary tool errors. If retrieval changes analytical confidence, describe the evidence limitation, not the debugging history.

For incomplete notes, distinguish confirmed metadata/abstract information from unverified analysis. Do not derive detailed methods, variables, hypotheses, sample construction, results, or robustness tests from an abstract. Mark important gaps in the section they constrain and link to supporting evidence without repeating the issue throughout the note.

## Extract with evidence and source discipline

Track evidence while reading; expose it in the form appropriate to the selected mode. Quick uses inline source locations, standard uses a selective Evidence Log, and deep uses a comprehensive log where useful. When using a log, assign stable claim IDs and link important factual assertions to them. Record paper version, printed page versus PDF page, section, equation, table/panel/column, figure, or appendix locator exactly as exposed. If pagination is absent, use real section labels and a short searchable excerpt; explicitly note unavailable locators. Never invent page or table references.

Prioritize conflicts in this order: paper full text; online/Internet appendix; official journal metadata; Zotero metadata; publisher page; abstract/database metadata. Apply this within the identified version; newer versions are not automatically evidence for older ones. Preserve a concise discrepancy record when higher-priority evidence corrects Zotero title/year/journal/DOI, including the original Zotero value and reason. Do not alter Zotero itself. Bibliographic identity keys remain Zotero/Better BibTeX identifiers.

Do not infer factual metadata from research conventions: CRSP does not establish country, Compustat does not establish an exchange universe, a DID estimator does not establish valid identification, and variable names do not establish construction. An untabulated robustness statement supports only the reported qualitative claim, not invented coefficients. Leave unverified YAML fields null/empty and explain consequential uncertainty in the body.

Keep authors' stated claims, verified numerical evidence, and your methodological interpretation distinct. Never invent sample sizes, variable definitions, coefficients, page numbers, table numbers, hypotheses, DOI, journal information, or data sources. Never infer causality from the authors' language alone. Use:
- `The paper does not clearly report this.` when the relevant source was read but is unclear.
- `Not verified from the available full text.` for unresolved fields.
- `I could not verify this from the available text.` when explaining a retrieval gap.
- `This appears to be inferred rather than explicitly stated by the authors.` for a labeled interpretation.
- `Not applicable.` only when the dimension does not apply, not when it is missing.

## Draft the note

Use concise academic English, neutral finance/accounting terminology, and compact paragraphs. When a passage is relatively long and contains separable points, steps, conditions, comparisons, or results, organize it as an itemized list when that improves readability. Use continuous prose when the argument depends on narrative continuity, and use tables only for genuine structured comparisons. Avoid praise and generic summary language. Distinguish statistical significance, economic magnitude, and substantive interpretation.

Adapt content to the paper type using the field guide: archival empirical, predictive ML, textual analysis, event study, asset pricing, experiment, survey, analytical/modeling, structural, qualitative, review, or conceptual. Prefer meaningful adaptations over lists of `Not applicable.` Retain the mode's core sections; standard must retain takeaway, question/gap, contribution, data/sample when applicable, design/method, results/arguments, literature position and summary. Explain key validity limits where they affect interpretation; avoid many tiny subsections.

Preserve comprehensive definitions of focal variables in deep mode; standard selects the central measures and quick gives only what is needed to understand the findings. Preserve the control-variable boundary in all modes: brief control blocks and specification locator only, without individual control definitions, formulas, sources, transformations, or coefficients.

For important empirical results, separate sign, statistical significance, economic magnitude, substantive interpretation, and important null/contrary evidence. A compact result table is useful when it compresses these distinctions. Do not convert broad author claims into universal support when reported tests conflict or are insignificant. Explain each substantive issue once; the Evidence Log supplies locators and concise evidence rather than repeating analytical paragraphs.

Follow the reference's YAML typing and conceptual distinctions. `primary_sample_size` describes a defensible primary analysis sample, not the raw database universe or an arbitrarily selected regression. Under Data and Sample, summarize the main count and unit, usually from the opening sample-construction subsection or primary sample table. Explain a necessary choice or unresolved ambiguity briefly. Put secondary counts in the relevant analysis only when useful; detailed test-specific counts are appropriate in deep replication-oriented reading, not a routine catalog in standard/quick. Do not guess rating, projects or country.

Include Position in Literature in standard/deep; quick may compress it. Identify actual closest papers, this paper's incremental contribution, and possible future research. Attribute comparisons based solely on the focal paper's literature review and distinguish proposed extensions from authors' claims. No invented papers, citation keys, links or relationships.

End the analytical content with Citation-Ready Summary, approximately 100-150 words of original synthesis covering question, data/sample, design, main finding, contribution and essential qualification. Use the mode's numbered heading from the reference; legacy unnumbered summaries remain valid on existing notes. With incomplete evidence, use fewer words as needed and qualify the synthesis. It must read as a paraphrase usable for later literature-review drafting.

## Obsidian template and existing-note safety

Inspect `<vault>/90_Templates/Paper Note.md` before drafting if accessible. Preserve useful custom fields and sections and align their conceptual roles with the authoritative reference. Report material schema conflicts; do not overwrite materially different customizations. Do not make routine paper reading silently redesign the vault template. During explicit setup/template alignment, create a missing manual fallback using the reference's standard body and shared YAML; [templates/Paper Note.md](templates/Paper%20Note.md) provides the aligned manual fallback. If the requested vault is inaccessible, report that rather than creating a different vault.

Before writing, resolve the absolute destination and verify it stays within `<vault>/10_Papers/`. Preserve the exact citation key and case. Reject path separators, traversal, Windows-invalid/reserved filenames, or case-insensitive collisions rather than silently sanitizing the key or editing Better BibTeX settings.

Apply the revised schema to newly generated notes and to existing notes only when the user explicitly requests an update. Do not bulk-migrate the vault or update a note as a side effect of skill revision. Preserve legacy properties such as `sample_size` and user-owned values; do not automatically rename or delete them.

If the destination exists, read it completely. Verify its Zotero item key and inspect any legacy note with the same item key if a citation-key change is suspected. Do not create duplicates or rename older notes automatically. Preserve unknown YAML fields and user-owned values (especially rating/projects), all manual prose/comments, `## My Notes`, and `<!-- USER NOTES START --> ... <!-- USER NOTES END -->` blocks verbatim.

New machine-authored notes use the generated-region markers in the reference. On update, replace only demonstrably generated material, preserving manual insertions even within a generated region. A marker is not permission to erase subsequent user edits. Without reliable provenance or a safe merge, leave the existing file unchanged and report a focused conflict/proposed replacement in the conversation. Do not append duplicate analytical sections.

Prepare and validate in memory or temporary storage before saving. Re-read the destination immediately before an update; if it changed since inspection, merge again. Use a safe replacement operation only after preserving manual content and passing checks. Do not overwrite on a failed check.

## Quality gate and delivery

Before saving:
- Check citekey equals the filename stem and verified Better BibTeX key; item key is the correct bibliographic parent.
- Reconcile title, year, journal, and DOI with Zotero; document source-backed corrections rather than forcing agreement.
- For a present DOI, validate syntax and correspondence to the paper using primary evidence (resolve when possible). Syntax alone is not identity validation; report unresolved issues.
- Verify primary sample and period against the source; distinguish raw universe, observations, entities, stacked rows and test-specific subsets. Never force a single count when none is defensible.
- Ensure methods, estimator, fixed effects, clustering, and causal language match the actual design.
- Trace main findings, signs, significance, units and magnitudes to evidence; retain important null/contrary results and check that source locations actually exist.
- Confirm full_text_status/status agree with coverage; mark unavailable appendices separately.
- Isolate YAML between the opening frontmatter delimiters and parse it using an available local YAML parser or equivalent reliable method when feasible. Correct syntax/indentation errors and reparse. Verify every shared-schema property is present, no duplicate keys, arrays for list fields, and the defined scalar types (including numeric counts); no accidental scalar/list conversions or unresolved drafting placeholders. A malformed frontmatter is a failed gate: never save it as complete. Reuse a suitable local parser; do not install a dependency solely for this check. If programmatic parsing is unavailable, perform an explicit type/syntax review and disclose that validation limitation in delivery.
- Check `reading_mode`; distinguish `paper_type`, `research_design`, `methods` and `identification_strategy`, with `noncausal` for verified noncausal work and no unsupported metadata.
- Check Markdown headings for duplicates outside code fences, generated/manual markers for balance, and manual content for preservation.
- Check mode-appropriate core sections, Position in Literature (standard/deep), and Citation-Ready Summary; verify all assertions respect the evidence ceiling.
- Remove redundant explanations and unnecessary execution/debugging details from the permanent note.

Save UTF-8 Markdown only after passing this gate. Report the final path, item and citekey, reading mode, full-text coverage, major source gaps, validation limitations and any merge conflict. Do not claim a note was saved if writing failed. Initial skill setup does not authorize creating a sample paper note.
