# Synthetic investigation fixtures

Nine illustrative cases define the proposed evidence boundary and scoring expectations. These are planning artifacts, not an implementation, benchmark result, runnable test suite, or production data. All environmental rules, dates, names and measurements are invented; they are not regulatory guidance. No Almic data, prompts or implementation were copied.

## Structure

- `observable/case-NNN.json`: only the complaint, declared task, observed evidence, recorded trace and missing artifacts. This is the entire investigator input.
- `private-oracle/case-NNN.json`: scoring-only labels, causal construction, expected counterfactuals, and regression specifications. Never include this directory in an investigator context, search index, tool response or model upload.

“Private” describes the intended evaluation role. It does not provide access control in this public illustration bundle. Every example is marked `benchmark_eligible: false` and `split: public-example-only`. An investigator that can read the repository can read the labels, so these files must never be used for a purported blind evaluation. Actual approved trials need fresh cases and isolated oracle storage.

The following index is also scoring/construction metadata and must not be passed to an investigator:

| ID | Family / purpose | Expected distinction |
| --- | --- | --- |
| case-001 | Wrong retrieved context | Correct arithmetic over another facility's rule |
| case-002 | Missing/outdated knowledge | Stale indexed rule despite newer authoritative version |
| case-003 | Unsupported complaint | Correct recorded computation; no defect established |
| case-004 | Model reasoning mistake | Incorrect conjunction with correct context |
| case-005 | Schema mapping failure | Correct model object corrupted by mapping |
| case-006 | App bug blamed on LLM | Stale rendered response; model processed revised input |
| case-007 | Insufficient evidence | Verdict and localization unresolved |
| case-008 | Multi-causal | Knowledge freshness and mapping independently fail |
| case-009 | Ambiguous localization | Symptom substantiated; model versus mapper unidentifiable |

## Claim decomposition

The adjudication unit is an atomic claim. Some natural-language complaints combine a symptom with a proposed cause. Case-006 deliberately contains both: the stale display is substantiated, while “the LLM ignored the edit” is unsupported. Its oracle explicitly requires that decomposition; a scorer must not treat one label as covering both claims. Case-009 supports the symptom while requiring localization abstention. Cases 006 and 009 include explicit `atomic_claim_labels` in the oracle; a production schema should carry atomic claim IDs and per-claim verdicts consistently. The headline adjudication field is not a substitute for those per-claim labels.

## Interventions and regression cases

All intervention records have `status: proposed_not_executed`. Their expected outcomes are private construction expectations, never actual test observations. They cannot justify claiming R2/R3 reproduction today. Initial fixtures include textual specs rather than executable tests; no tests, application or model calls were run. The later approved technical experiment must execute actual isolated seeded-fault baseline/intervention/restoration replays and expose the observed outcomes without oracle explanations. Pre-authored expectations alone cannot validate experimental root-cause diagnosis. That harness does not exist here.

Regression specifications describe both faulty and healthy variants. At evaluation time a generated regression must be assessed against independent variants; repeating the same example or using the oracle as the regression answer key is not generalization evidence.

## Future split policy

Do not assign these public illustrations to train/dev/held-out partitions. Author fresh data for the proposed 60 train / 60 dev / 240 held-out base incidents. Split causal templates, source/entity sets and paraphrase lineages before generating variants; keep all descendants of a base incident together. High-level categories recur across splits, but held-out template families and mechanism variations must be genuinely unseen. Report results by category, negative-case type and data provenance. See `../../docs/EVALUATION-STRATEGY.md` for budgets, confidence intervals and stop/pivot gates.

## Inspection checklist

- Each observable ID has one matching oracle ID.
- All JSON parses; evidence references resolve within the observable record.
- Observable filenames/IDs carry no root-cause labels or split hints.
- Missing evidence remains missing; scoring permits abstention.
- Fixture facts and counterfactuals are internally consistent.
- Public examples never become scored holdout cases.

## Coverage gaps

The nine pairs illustrate the six requested scenario families and several uncertainty cases. They do not yet supply malicious-instruction, stochastic drift, or baseline-nonreproduction cases. Those cases are required before an approved evaluation can claim the broader safety/reproducibility coverage in REQUIREMENTS.md. No acceptance benchmark has been run.
