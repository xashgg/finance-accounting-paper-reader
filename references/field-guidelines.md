# Finance and accounting extraction guide

Use the core checklist for every paper and only the design/type modules that apply. These are reading questions and red flags, not required tests that every paper must perform. Use them as analytical checks in every mode; output depth and evidence-log size are controlled by SKILL.md and the note-schema reference. Quick retains central evidence and qualifications, standard selects consequential design details, and deep develops applicable replication detail. Record what authors actually do, then assess what it establishes; never fill missing details with standard practice.

## Core scope and reading priorities

Primary orientation: Journal of Finance, Journal of Financial Economics, Review of Financial Studies, Review of Finance, Journal of Financial and Quantitative Analysis; The Accounting Review, Journal of Accounting Research, Journal of Accounting and Economics, Review of Accounting Studies, and Contemporary Accounting Research. Apply the same evidence discipline to related economics, management, entrepreneurship, and information-systems papers. Venue does not determine quality or paper type.

- Research question: identify the economic object, decision-maker, friction, outcome and counterfactual. Explain the stakes without adding unsupported practical claims.
- Literature gap: distinguish what the authors claim from what you independently establish. Classify theoretical, empirical, measurement, institutional or identification gaps.
- Contributions: assess theoretical, empirical, identification, measurement/data and institutional contributions separately. A new setting alone is not necessarily a new mechanism.
- Theory: extract named theories, assumptions, mechanism, formally stated hypotheses and competing predictions. Distinguish authors' theory from your interpretation; do not invent a hypothesis from an observed sign.
- Institutions: record law/rule/standard names, jurisdiction, affected entities, thresholds, enforcement, announcement versus effective dates, phase-ins, exemptions and overlapping reforms. Explain exposure/compliance and why variation could identify the claimed effect. Interpret rules as of the study period.
- Data: verify country/market, universe, time span, observational unit, final counts, distinct entities, cluster counts, merge keys and losses, screens, delistings, missingness, and sample attrition. Distinguish database universe, screened primary analysis sample, unique entities and stacked observations; resolve model/subsample differences while reading. The note summarizes the defensible primary sample, with secondary counts in the relevant analysis only when useful; deep mode may include detailed counts for replication. No arbitrary count is required when there is no single primary sample.

## Common data sources: what to verify

Treat this list as search cues, never evidence that a paper used a source.

| Source | Extraction questions |
|---|---|
| CRSP | Security/share/exchange coverage, returns versus prices, delisting returns, identifier history and calendar alignment |
| Compustat | Annual/quarterly files, accounting item definitions, consolidated entities, fiscal-year alignment, restatements and point-in-time availability |
| IBES / I/B/E/S | Detail versus summary files, forecast horizon, actuals, split adjustments, analyst identifiers and forecast timing |
| Audit Analytics | Audit opinions/fees, restatements, internal controls or other modules; event definition and database coverage |
| BoardEx | Director/executive identities, affiliations, network dates, coverage and entity matching |
| EDGAR | Filing forms, accession/version, filing acceptance date, amendments, extraction unit and availability timestamp |
| Capital IQ, Refinitiv, FactSet | Exact product/module, coverage, field definitions, ownership/security identifiers and historical vintages |
| TRACE | Bond universe, transaction filters, corrections/cancellations, reporting rules, size caps and dissemination timing |
| DealScan | Facility versus package, borrowers/lenders, contract dates, amendments and links to accounting data |
| SDC | Deal type/status, announcement/completion, withdrawn transactions and coverage restrictions |
| ExecuComp | Executive role, compensation components, option/equity valuation and firm coverage |
| RavenPack | News source universe, relevance/novelty scores, timestamps, entity assignment and model version |
| Glassdoor | Review timestamp, employee selection, moderation, employer matching and coverage |
| Hand-collected/proprietary data | Source documents, collection protocol, coding rules, coder agreement, missingness, access and reproducibility |

Do not assume familiar database acronyms imply familiar samples, variable definitions or licensing/accessibility. CRSP does not establish a country and Compustat does not establish an exchange universe. Leave metadata empty when unverified; a familiar variable label does not establish its construction. For merged sources inspect one-to-many joins, changing identifiers and duplicate handling.

## Focal variable construction

For dependent, main independent, mediator/moderator and alternative focal measures, extract:
- Concept, operational definition, formula as reported, underlying items and source.
- Unit, sign convention, denominator, aggregation, time alignment, lags and measurement window.
- Scaling, logs (including zero handling), winsorization/trimming thresholds and grouping, standardization, deflation and missing-value handling.
- Construct justification, validation and limits. Distinguish economic construct from its proxy.

Do not supply textbook definitions of accruals, conservatism, investment efficiency, constraints, disclosure quality, liquidity or risk if the paper uses its own implementation. Ratios may mechanically share denominators; estimated/generated measures may embed first-stage error. Check whether treatment changes observability or coding rather than the underlying construct.

Control variables receive only a block-level summary and specification reference. Do not catalogue their definitions, formulas, data sources, transformations or coefficients.

## Panel specifications, fixed effects and inference

Extract the stated equation if legible; otherwise summarize verbally. Record estimator (OLS, logit/probit, Poisson, hazard, etc.), estimand, focal terms/interactions, controls as blocks, weights, lag structure and estimation sample. Explain main effects conditional on interactions; do not interpret an interaction coefficient alone as a total effect.

For fixed effects, specify absorbed dimensions and interactions precisely: firm plus year differs from firm plus industry-by-year. Identify remaining variation, absorbed treatment/main effects, singleton losses and possible lack of within-unit variation. Fixed effects do not remove time-varying confounding by themselves.

For inference, record heteroskedasticity correction, clustering dimension(s), number of clusters when reported, treatment-assignment level, temporal/spatial dependence, bootstrap method and small-cluster adjustments. Check mismatch between identifying variation and inference level. Do not assume firm clustering or add an unreported correction. Extract estimator-specific marginal effects when relevant; coefficients of nonlinear models are not automatically probability changes.

## Difference-in-differences, event studies and triple differences

Extract treatment, eligibility/exposure, announcement/effective dates, first treatment, reversals, intensity, treated/control groups and target effect. Distinguish never-treated, not-yet-treated and already-treated comparisons.

Look for:
- Source of identifying variation and the relevant parallel-trends assumption, conditional covariates and common support.
- Event-time construction, omitted period, leads/lags, endpoint binning, confidence intervals and simultaneous versus pointwise inference.
- Anticipation, spillovers, contamination, changing sample composition and concurrent reforms.
- Staggered adoption: estimator, comparison cohorts, cohort/time aggregation and treatment-effect heterogeneity; whether already-treated comparisons or problematic weighting affect interpretation.
- Pretrend estimates and power; an insignificant pretrend test does not prove parallel trends.
- Timing endogeneity, differential shocks and treatment assignment.
- Triple differences: the third comparison dimension and the additional differential-trend assumptions; a third difference does not automatically solve confounding.

Keep dynamic DID event studies distinct from corporate announcement-return event studies.

## Instrumental variables

Record instrument formula, source, level, timing, endogenous regressor, first-stage equation/result and sample; reduced form and second stage where reported. Identify relevance, exclusion restriction, independence and any monotonicity/complier interpretation required.

Extract the actual weak-instrument statistic and inference method; do not label every first-stage F statistic equivalent or apply a universal cutoff without context. Look for weak-IV-robust inference, multiple instruments, overidentification evidence and heterogeneous-effect interpretation. First-stage strength and overidentification tests do not prove exclusion. Discuss plausible direct channels, common shocks, exclusion failures and whether fixed effects leave relevant variation.

## Regression discontinuity

Extract running variable, cutoff, assignment rule, sharp/fuzzy design, compliance, bandwidth choice, kernel, polynomial/local fit and bias/inference treatment. Identify which local population the estimate describes.

Check manipulation/sorting/density evidence, covariate continuity, other policies at the threshold, bandwidth sensitivity, discrete running variables, donut restrictions and functional-form dependence. A discontinuity in outcomes alone is not a validated design; balance and density tests also do not prove every assumption.

## Matching and reweighting

For propensity-score matching, entropy balancing or other approaches, record treatment, target estimand (e.g. ATT/ATE), pre-treatment covariate blocks, algorithm, calipers, replacement, trimming, support, balance metrics and effective sample sizes/weight concentration. Keep control-variable construction out of the note.

Check post-treatment variables, remaining imbalance, overlap, extreme weights and inference after design estimation. Matching/reweighting addresses observed differences under assumptions; it does not automatically eliminate unobserved confounding. For matched DID inspect both design stages.

## Other identifying designs

- Natural experiment / policy shock / geographic variation: specify assignment and exposure, endogenous location/sorting, spillovers, spatial inference and competing events; "natural" is not an identifying assumption.
- Peer effects: distinguish endogenous peer response, contextual effects and shared environment; check reflection, network formation, leave-one-out construction and common shocks.
- Shift-share: extract shares, shocks, base years, leave-out construction, which component supplies exogeneity, concentration and inference appropriate to correlated exposures.
- Synthetic control: donor pool, pre-treatment fit, predictor/outcome windows, weights, contamination, placebo inference and sensitivity to influential donors.
- Selection or simultaneous-equation models: selection equation, exclusion restrictions, distributional assumptions and which selection mechanism is addressed.

## Asset pricing: portfolio sorts and Fama–MacBeth

Portfolio sorts: signal definition, information availability, formation/holding dates, breakpoints/universe, independent versus conditional sorts, rebalancing, value/equal weighting, long/short legs, microcaps, missing returns, delisting and turnover. Check look-ahead, survivorship and selection bias.

Extract factor models, benchmark/factor versions, excess versus raw returns, factor-adjustment windows, alpha units/frequency and uncertainty. Distinguish predictive return spreads, abnormal returns relative to a model, priced risk and causal effects.

Fama–MacBeth: first-stage objects if any, repeated cross-sectional regression frequency, regressors/signals and timing, coefficient averaging, time-series inference/HAC lags and generated-beta corrections if reported. Do not equate it with pooled OLS. Inspect short-sale feasibility, transaction costs, liquidity, capacity and whether net returns are calculated or merely discussed.

## Corporate event studies

Record event definition/source; event date and time (including after-hours alignment); estimation and event windows; expected-return model and benchmark; abnormal return measure (AR, CAR, BHAR); overlapping/multiple events; confounding announcements; and inference under cross-sectional dependence.

Distinguish daily/cumulative from buy-and-hold measures and their units. Short-window reactions can be consistent with revised expectations without identifying a particular mechanism or long-run real outcome. Address leakage, anticipation, endogenous event occurrence and benchmark sensitivity where relevant.

## Textual analysis and machine learning

Extract source documents, sampling and timestamps, text unit, language, preprocessing/tokenization, dictionary/model and version, label definitions, coding procedure, annotators/agreement, training data, validation/test data, split scheme, hyperparameter selection and performance metrics.

Check:
- Separation of training, tuning and untouched test data; time/entity/document overlap and duplicate leakage.
- Information actually available at prediction time; future labels or revised documents.
- Pretrained-model provenance, training cutoff if known, prompt/model settings and nondeterminism when applicable.
- Class imbalance, calibration, baseline comparisons, uncertainty and performance across periods/entities/subgroups.
- Construct validation beyond predictive accuracy; domain shift and genuinely out-of-sample validation.
- Reproducible code, model/data access, seeds and API/model version drift.

For text-derived regressors, connect prediction/coding errors to measurement error and downstream inference. Predictive performance or feature importance is not causal identification. Do not invent unreported training details or treat a random split as temporal external validation.

## Mechanisms, heterogeneity and robustness

For each mechanism: proposed channel, proxy, design/test, result with evidence, and competing mechanisms actually distinguished. Mediation, attenuated coefficients after adding a mediator, and supportive subgroup patterns do not establish a causal channel without additional assumptions. Examine post-treatment conditioning and mediator-outcome confounding.

For heterogeneity: partition/moderator, rationale, timing, thresholds, interaction or formal between-group test, results and relation to theory. Significance in one subgroup and insignificance in another is not evidence that the effects differ. Note exploratory multiplicity or power limits when supported.

Classify each robustness exercise by threat addressed:
- Measurement: alternative dependent/independent focal measures.
- Sample: exclusions, restrictions, missingness, influential observations.
- Specification/inference: alternative fixed effects, clustering, functional forms.
- Timing: alternative windows/lags and anticipation.
- Falsification: placebo dates, outcomes/groups, negative controls.
- Design: matching/reweighting or alternative identification.
- Confounding: additional control blocks, competing events or omitted exposures.

For each category extract implementation, result/location and what threat remains. A long list of similar regressions is not independent proof of identification.

## Endogeneity and validity

Explicitly assess omitted variables, reverse causality, measurement error, selection, simultaneity and endogenous treatment timing; distinguish addressed, partly addressed, unresolved, unassessed and inapplicable concerns.

- Internal validity: credible comparison, assignment, confounding, interference, attrition, timing.
- External validity: population, market, regime, time, support, local/complier effects and feasible transportability.
- Construct validity: proxy validity, reporting incentives, coding reliability, mechanical relationships.
- Statistical conclusion validity: dependence/inference, effect uncertainty, power, multiple comparisons, specification search and model fit where applicable.

Do not infer absence of a problem from absent discussion, or a demonstrated problem from an unperformed diagnostic. Separate author-acknowledged limitations from your conditional concerns.

## Economic versus statistical significance

Report sign, estimate and uncertainty separately from substantive interpretation. Preserve units, scaling, model/column, outcome baseline and sample. Convert magnitudes only with verified inputs; label your calculation and show its basis. A standardized coefficient requires the appropriate standard deviation; percentage points differ from percent changes; log and nonlinear-model interpretations require care.

Record exact p-values only when given; stars generally support thresholds, not exact values. An insignificant estimate does not establish no effect, and a large point estimate with wide uncertainty is not a precise economic conclusion. Do not backfill missing numbers from narrative adjectives.

For the main findings, report the strongest supporting evidence alongside important null,
contrary or boundary findings. A compact table can separate sign, statistical significance,
economic magnitude and substantive interpretation. Do not let broad claims of superiority
override mixed table evidence. Untabulated robustness statements do not supply unreported
coefficients. Explain major inconsistencies once where they affect interpretation.

## Position in literature

Identify the closest papers actually named in the focal paper or otherwise verified in
authorized sources. Compare their question, setting, design or measurement with the focal
paper; label comparisons based solely on its literature review. Distinguish the authors'
claimed contribution, your source-grounded assessment and your proposed future extensions.
Do not fabricate papers, links, citation keys or research relationships. Keep this synthesis
distinct from the user's personal research relation, which needs actual project context.

## Adaptation beyond archival empirical work

- Experimental: design, recruitment, randomization unit, manipulations, incentives, checks, outcomes, exclusions/attrition, preregistration if reported, demand effects, power and internal/external validity.
- Survey: sampling frame, response/selection, instrument/scales, construct reliability/validity, response rate, common-method concerns and weights.
- Analytical/modeling or conceptual/theory: primitives, assumptions, timing, equilibrium, propositions/proofs, comparative statics, boundaries, competing models and testable implications. Empirical sample/regression sections may be inapplicable.
- Structural: model primitives, identifying moments/variation, estimation/calibration, objective, parameter uncertainty, fit, validation and counterfactual assumptions. Distinguish identification from fit and calibrated from estimated parameters.
- Qualitative: setting/case selection, access, interviews/documents, coding, triangulation, positionality and analytic generalization; do not force statistical representativeness.
- Literature review: scope, search sources/dates, inclusion criteria, synthesis logic, theoretical organization and coverage limitations; do not claim systematic methods unless reported.
- Meta-analysis: eligibility, effect-size harmonization, dependence, weighting/model, heterogeneity, publication/selection bias, moderator analyses and sensitivity; distinguish papers/studies/effects/participants.

Hybrid papers may need more than one module. Place relevant specifics within Data, Empirical Design, Results and Limitations using descriptive subheadings; preserve core schema and avoid duplicate sections.
