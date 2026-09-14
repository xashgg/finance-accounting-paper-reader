---
type: paper
citekey: null
zotero_item_key: null
title: null
authors: []
year: null
journal: null
volume: null
issue: null
pages: null
doi: null
url: null
zotero_uri: null
zotero_library: null
field: []
topics: []
theories: []
paper_type: []
research_design: []
methods: []
identification_strategy: []
data_sources: []
country: []
sample_period: null
unit_of_analysis: null
primary_sample_size: null
reading_mode: standard
status: unread
rating: null
projects: []
date_read: null
full_text_status: null
---

# Paper-note output schema

This reference defines the shared frontmatter and mode-specific bodies. The YAML block
above is the canonical schema for every newly generated note; preserve every property
in quick, standard and deep modes. Combine it with one body below. The blank manual
fallback uses standard mode and unread/null coverage until a reading is completed.
Do not copy this reference's explanatory sections into a research note.

## YAML property contract

| Properties | Required type and meaning |
|---|---|
| type | String, always `paper` |
| citekey, zotero_item_key, title, journal, volume, issue, pages, doi, url, zotero_uri, zotero_library | String or null; quote numeric-looking volume/issue/pages |
| authors, field, topics, theories, paper_type, research_design, methods, identification_strategy, data_sources, country, projects | Arrays of strings; unknown values are `[]`, never a scalar string |
| year | Integer or null |
| sample_period, unit_of_analysis | Short string or null; explain important multiple periods/units in the body |
| primary_sample_size | Positive integer observation count or null |
| reading_mode | String: `quick`, `standard` (default), or `deep` |
| status | String: `unread` for a blank template; `read` for complete quick/standard; `deep-read` for complete deep; `partial-read` or `metadata-only` for incomplete evidence |
| full_text_status | `available`, `partial`, `unavailable`; null only in an unread manual template |
| rating | Number or null for new notes; do not assign without user input |
| date_read | Quoted ISO date string `YYYY-MM-DD` or null before reading; an Obsidian date property |

Mode and coverage are independent: a requested deep note can be partial-read, and quick
mode can read the full article. Existing `status: deep-read` notes remain valid; do not
reinterpret their historical depth automatically.

### Classification properties

- **paper_type:** what kind of paper it is, e.g. `archival empirical`, `predictive machine learning`,
  `analytical/modeling`, `survey`, `qualitative`, `literature review`, `conceptual`.
- **research_design:** broad design, e.g. `difference-in-differences`, `event study`,
  `temporal holdout`, `forecast comparison`, `return association`, `portfolio analysis`.
- **methods:** estimators/algorithms, e.g. `OLS`, `k-nearest neighbors`,
  `Fama-MacBeth regression`. Do not infer a method from an ambiguous caption.
- **identification_strategy:** verified source of causal identifying variation,
  e.g. `staggered regulatory adoption`; its validity still needs assessment.
  Use `[noncausal]` for a verified prediction/association/noncausal paper.
  Use `[]` when not verified, not `[noncausal]` as a default guess. For mixed papers,
  describe verified causal variation here and distinguish noncausal exercises in the body.

Use concise, consistent labels; do not mix descriptions of prediction designs into
causal identification. Named databases, variable labels and customary study practices
are not evidence for country, exchange universe, construction or identification validity.

### Primary sample and compatibility

Populate `primary_sample_size` only when a defensible primary analysis sample exists,
normally corroborated by initial data/sample-construction text or the main sample table.
Distinguish the initial database universe from the post-screening analysis sample.
Multiple supplementary tests do not by themselves make a primary sample impossible.
Where several coequal samples have no defensible single count, use null and explain
briefly; do not sum incompatible samples, conflate stacked rows with firms, or guess.

New notes use `primary_sample_size` in place of legacy `sample_size`. On an explicitly
requested update, preserve existing `sample_size` and unknown/user-owned properties.
Add the new property from verified evidence; do not silently copy a legacy value with
unclear meaning or delete/rename the old property. Preserve user rating/projects values.
Schema changes alone never authorize bulk migration or rewriting existing notes.

## Shared body conventions

- Use concise academic English. Convert relatively long passages into itemized lists
  when they contain separable points, steps, conditions or results. Use tables for
  compact comparisons; do not fragment a coherent argument into tiny subsections.
- Explain each substantive issue in its most relevant analytical section once. Cross-reference
  only as needed; Evidence Log entries provide short evidence and locators.
- Important results retain direction, uncertainty/significance, economic magnitude,
  interpretation and material null/contrary evidence in every mode.
- Preserve paper-type-appropriate core content. Standard keeps its section roles even
  when adapting Research Design to Method and Main Results to Main Arguments. A
  conceptual/modeling paper may discuss primitives or its evidence base under Data and
  Sample; use `Not applicable.` sparingly and never as a substitute for unverified.
- Position in Literature is mandatory in standard/deep, with the three subheadings
  shown below. Quick may integrate a short paragraph into question/gap or findings.
  Use only identified papers; attribute focal-paper-only literature comparisons.
- Citation-Ready Summary is the last analytical section, 100-150 original words when
  evidence supports it, with question, data/sample, design, finding, contribution and
  essential qualification. Use the numbered heading for the selected mode. Accept
  legacy unnumbered headings during safe updates without duplicating the summary.
- Generated content stays between generated markers. Always end with the exact My Notes
  heading and user markers shown below; preserve all user-authored content verbatim.
- Replace drafting comments/placeholders in generated notes; empty evidence tables
  should be replaced with a concise availability statement.

### Optional Reading Record

Quick normally omits it. Standard normally omits it or uses at most a few short bullets
under an unnumbered `## Reading Record` before the takeaway:

- Full text: Available / Partial / Unavailable.
- Version: Verified version, or unknown.
- Source: Zotero PDF / identified primary source.
- Coverage: Main article and the appendices actually read.
- Verification issues: Only consequential issues; refer to the analytical discussion.

Deep may expand this record for methodologically useful source/version/appendix coverage.
Never preserve MCP call failures, attachment-path debugging, HTTP 403 responses,
token/display limits, extraction implementation details, copyright-page details or
temporary errors merely because they occurred. Include a substantive limitation such
as an unreadable equation or unavailable appendix when it affects confidence, without
its troubleshooting chronology.

## Standard body (default; manual fallback)

Use the shared YAML above plus this body. Approximately 2,000-3,500 body words is
guidance for a typical empirical paper, not a hard cap. Select key evidence rather than
reconstructing every exhibit.

```markdown
# {{title}}

<!-- GENERATED CONTENT START -->

## 1. One-Sentence Takeaway

<!-- Question, main answer and essential qualification. -->

## 2. Research Question and Gap

<!-- Economic object and stakes; authors' claimed gap, clearly attributed. -->

## 3. Contribution

<!-- Relevant theoretical, empirical, methodological, measurement or institutional
contributions. Distinguish authors' claims from your assessment; avoid empty categories. -->

## 4. Theory

<!-- Mechanism, assumptions, competing predictions and actual hypothesis labels.
For non-theory papers, explain the conceptual rationale without inventing hypotheses. -->

## 5. Data and Sample

<!-- Sources, verified market/country, period, unit, key screens and a defensible main
analysis count. If using a Final Sample Size subheading, keep it to that primary count
and unit. Do not routinely enumerate every regression/horizon/subsample count.
For analytical/conceptual papers discuss the model setting or evidence base as appropriate. -->

## 6. Variable Construction

<!-- Central dependent, focal independent, mediator/moderator and alternative measures:
actual definitions, timing, units, scaling and consequential missingness/transformation.
Use a compact table if helpful. Controls: brief blocks and specification locator only. -->

## 7. Research Design and Identification

<!-- Actual method, estimator/algorithm, key specification, comparison and assumptions.
Report fixed effects and clustering when applicable; distinguish causal identification
from prediction/association. ML: temporal availability, train/tune/test splits and metrics.
Integrate consequential endogeneity, selection and validity concerns here once. -->

## 8. Main Results

<!-- Separate sign, significance, economic magnitude, interpretation and important null
or contrary findings. Use a compact table when helpful. For theory/reviews, adapt to
Main Arguments: propositions, synthesis and boundaries, without fabricated statistics. -->

## 9. Mechanism and Heterogeneity

<!-- Channel/proxy/test/result, competing channels and limits of mechanism evidence.
Distinguish within-group significance from a formal between-group difference. -->

## 10. Robustness

<!-- Select major threats, responses, results and remaining limitations.
Untabulated claims are qualitative unless actual outputs are available. -->

## 11. Position in Literature

### Closest Papers

<!-- Name only actually identified papers; say when based solely on the focal paper's
literature review. Do not invent citation keys or links. -->

### What This Paper Adds

<!-- Compare with those papers; reference Contribution rather than repeating it. -->

### What Future Research Can Build On

<!-- Source-grounded opportunities and constraints; label your proposed extensions. -->

## 12. Evidence Log

| Claim | Source Location | Evidence |
|---|---|---|

<!-- Usually 5-12 selective entries: main sample, central measures, design, findings,
major mechanism/robustness evidence. Use stable anchors, e.g. <a id="e1"></a> E1,
linked from analysis as [E1](#e1). Exact version and actual page/table/figure/equation/
appendix locations only. Brief evidence, not repeated analytical paragraphs.
Label abstract-only evidence and material source uncertainty. Remove empty tables. -->

## 13. Replication Resources

<!-- Verified data/code/repository links and access conditions; separate appendix
availability and coverage. Distinguish resources identified from inspected or executed.
Discuss only material replication gaps, referring to earlier analysis where appropriate. -->

## 14. Citation-Ready Summary

<!-- About 100-150 words of original synthesis: question, data/sample, design, main
finding, contribution and essential qualification. Qualify incomplete evidence.
Last analytical section; do not format as a quotation. -->

<!-- GENERATED CONTENT END -->

## My Notes

<!-- USER NOTES START -->

<!-- USER NOTES END -->
```

## Quick body

Use exactly the same shared YAML properties/types; set `reading_mode: quick`.
Target about 800-1,500 body words, excluding YAML. Read the full paper when readily
available but synthesize selectively. Provide inline source locations for central
claims instead of a full Evidence Log. Do not reconstruct tables unless necessary
to explain a central result or qualification.

```markdown
# {{title}}

<!-- GENERATED CONTENT START -->

## 1. One-Sentence Takeaway

## 2. Research Question and Gap

## 3. Data and Sample

## 4. Research Design / Method

## 5. Main Findings

<!-- Prioritize the answer and important null/contrary results. Include compact real
source locations inline, e.g. printed p. 129, Table 5, only when verified.
Literature position may be one short paragraph naming genuinely identified comparators. -->

## 6. Citation-Ready Summary

<!-- About 100-150 words, original synthesis with essential qualification. -->

<!-- GENERATED CONTENT END -->

## My Notes

<!-- USER NOTES START -->

<!-- USER NOTES END -->
```

## Deep body

Use exactly the same shared YAML properties/types; set `reading_mode: deep`.
Retain the established detailed structure below, adapting subsections when needed.
Cover applicable focal definitions, sample construction, specifications, identifying
assumptions, fixed effects, clustering, magnitudes, null/contrary findings, robustness
taxonomy, endogeneity, mechanism validity, replication concerns, reporting inconsistencies,
exhibit mapping and supplementary coverage. No rigid word limit; avoid repetition and
irrelevant operational detail. Evidence entries should be comprehensive where useful,
not manufactured to fill a quota.

```markdown
# {{title}}


<!-- GENERATED CONTENT START -->

## 0. One-Sentence Takeaway

<!-- Question, central finding, and design-appropriate interpretation in one sentence. -->

## 1. Research Question

<!-- Exact question; economic phenomenon; why it matters. -->

## 2. Literature Gap

<!-- Authors' claimed gap; classify theoretical/empirical/measurement/institutional/
identification gap. Do not present the claimed gap as an independently verified literature review. -->

## 3. Contribution

### Theoretical Contribution

### Empirical Contribution

### Identification Contribution

### Measurement / Data Contribution

### Institutional Contribution

<!-- Separate authors' claims from your assessment in each applicable subsection. -->

## 4. Theory and Hypotheses

### Theoretical Mechanism

<!-- Explicit named theories and authors' causal chain; label your interpretation. -->

### Hypotheses

<!-- Preserve actual hypothesis labels, direction, conditions, and source locations.
If none are formally stated, say so; do not invent numbered hypotheses. -->

### Competing Explanations

## 5. Institutional Setting

<!-- Relevant laws, regulations, accounting standards, exchange/disclosure rules,
reforms/shocks, announcement and effective dates, and relevance to identification.
Describe the rules in the study period; do not silently substitute current rules. -->

## 6. Data and Sample

### Data Sources

<!-- Country/market; provider, product, coverage; proprietary or hand-collected inputs. -->

### Sample Construction

<!-- Universe, merges, screens, exclusions, missingness, attrition and selection. -->

### Sample Period

### Unit of Analysis

### Final Sample Size

<!-- Summarize the defensible primary analysis count and unit. Explain an ambiguity
rather than selecting an arbitrary count. Place detailed secondary test counts in the
relevant design/result/replication discussion when they serve deep reading. -->

## 7. Variable Construction

### Dependent Variables

### Main Independent Variables

### Mediators / Moderators

### Control Variables

<!-- Brief control-block summary and specification locator only.
Do not record individual control definitions, formulas, transformations, sources or coefficients. -->

### Alternative Measures

<!-- For focal variables only: concept, operational definition/formula, source,
timing, units, transformations/winsorization, missing-value treatment, evidence locator.
Use compact per-variable tables if helpful; do not assume customary definitions. -->

## 8. Empirical Design

### Baseline Specification

<!-- Actual equation or accurate verbal specification; estimator, outcome, focal
regressors, control blocks, weights and lags. Never manufacture an equation.
Add design-specific subsections here (DID, IV, RDD, event returns, pricing, text/ML,
experiment, structural model, etc.) using field-guidelines.md. -->

### Identification Strategy

<!-- Identifying variation; comparison group/counterfactual; target estimand. -->

### Fixed Effects

### Standard Errors / Clustering

### Identification Assumptions

### Endogeneity Concerns

<!-- Address omitted variables, reverse causality, measurement error, selection,
simultaneity, endogenous timing; authors' response and remaining threats separately. -->

## 9. Main Results

### Statistical Results

<!-- Focal estimate/sign, uncertainty or reported significance, and model/table/
panel/column. Distinguish reported p-values from threshold/star evidence. -->

### Economic Magnitude

<!-- Units, baseline/scaling and comparison; show transparent calculations if derived. -->

### Interpretation

<!-- Match causal/associational language to design; distinguish null from inconclusive. -->

## 10. Mechanism Tests

<!-- Channel -> proxy -> test -> result -> alternatives distinguished or unresolved. -->

## 11. Cross-Sectional / Heterogeneity Tests

<!-- Partition variable, rationale, comparison result, formal difference test and
whether it supports the proposed mechanism. -->

## 12. Robustness Tests

<!-- Classify by measurement, sample, fixed effects, clustering, timing, placebo/
falsification, matching/reweighting, identification, confounders, competing events,
functional form. For each, explain the threat, implementation, result and limitation. -->

## 13. Tables and Figures

| Table/Figure | Purpose | Main Finding |
|---|---|---|

<!-- Inventory actual main-paper tables/figures and consulted appendix exhibits.
Include panel/column/version when needed; identify unread or unreadable exhibits. -->

## 14. Limitations

### Internal Validity

### External Validity

### Construct Validity

### Statistical Conclusion Validity

<!-- Separate authors' acknowledged limitations from your evidence-based assessment.
Do not label an unperformed test a demonstrated flaw or claim causal proof. -->

## 15. Evidence Log

| Claim | Source Location | Evidence |
|---|---|---|

<!-- Start Claim cells with stable anchors, e.g. <a id="e1"></a> E1: [actual claim].
Locations must exist: version; printed p. / PDF p.; section; table/panel/column, etc.
Evidence is a short faithful excerpt or precise numerical paraphrase with units and
model context, not merely "baseline regression." Label abstract-only evidence.
Record version and material evidence gaps briefly. A useful optional Reading Record
may link to the affected analysis; do not repeat the same methodological concern.
Retain existing IDs on updates; update incoming references if an ID must change. -->

## 16. Replication Resources

### Data

### Code

### Online Appendix

### Repository

<!-- Verified links/access restrictions, version/access date when relevant.
Distinguish a linked repository from code actually inspected/run. Never imply replication
was performed simply because materials exist. Under Online Appendix, state whether a
separate appendix was available and inspected when that affects the evidence ceiling. -->

## 17. Position in Literature

### Closest Papers

<!-- Only actually identified papers; attribute focal-paper-only comparisons. -->

### What This Paper Adds

<!-- Specific comparison; refer back to Contribution as needed. -->

### What Future Research Can Build On

<!-- Separate authors' agenda from your proposed extensions and their conditions. -->

## 18. Citation-Ready Summary

<!-- Approximately 100–150 words: research question, data, empirical strategy,
main finding, contribution. Original paraphrase; evidence-qualified, no invented detail.
This is the last analytical section; user notes may follow outside the generated region. -->

<!-- GENERATED CONTENT END -->

## My Notes

<!-- USER NOTES START -->

<!-- USER NOTES END -->
```
