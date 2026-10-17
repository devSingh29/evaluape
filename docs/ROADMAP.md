# Evidence-gated roadmap

This is a sequence of decisions, not committed dates or authorization to execute. Effort estimates require discovery; no implementation or experiment has run.

| Phase | Deliverable | Exit evidence | If the gate fails |
| --- | --- | --- | --- |
| 0. Problem and competitor validation | Interviews, task definition, verified competitor capability matrix, neutral evidence contract | A recurring complaint-investigation job inadequately served by existing tools; explicit incremental hypothesis | Stop or narrow to an integration/export workflow |
| 1. Evaluation design | Fresh synthetic dataset, private oracle isolation, reviewer rubric, strong baselines, preregistration and approved budget | Leakage audit passes; feasible evidence; sufficiently powered design or clearly exploratory designation | Repair cases or reduce claims before code |
| 2. First approved experiment | Frozen equal-budget comparison, actual isolated seeded-fault controlled replays, and ablations under EVALUATION-STRATEGY.md | Diagnostic uplift, useful coverage, accusation bound and cost gates met | Pivot to LLM-only workflow or deterministic niche; no superiority claim |
| 3. Human-reviewed MVP | One intake format, reviewable diagnosis, issue export and regression specification | Engineers can act on artifacts; reproducible evidence; review savings across new cases | Remove steps that add no measured value |
| 4. Small external pilot | Consented redacted incidents from at least two independently operated applications and different failure mechanisms | Benefits survive real evidence gaps; no unsafe blame; users return voluntarily | Revisit generalization and evidence acquisition |
| 5. Low-friction adoption | Versioned package, documented uninstall, one separately authorized read-only connector | Setup burden is lower than demonstrated recurring benefit; privacy/security review passes | Keep manual imports and avoid integration sprawl |
| 6. Selective expansion | Additional formats/domains justified by observed demand | Fresh holdout and safety checks for each material expansion | Maintain bounded scope |

## Non-goals throughout this roadmap

No autonomous fixing, merging or production mutations. No full observability suite, hosted dashboard, broad platform replacement, or automatic customer-facing blame. These need separate product hypotheses, explicit authorization and evaluation, not an automatic next phase.

## Decisions required before execution

- Who owns fixture review, adjudication disagreements and final go/no-go?
- Which model/version, tool budget, maximum USD spend and data-processing terms are approved?
- Can the primary claim be powered within that budget? If not, what narrower exploratory question is valuable?
- What evidence can a pilot participant actually export safely and cheaply?
- Which existing trace/eval products should be integrated with rather than duplicated?

## Release discipline

Keep public illustrations separate from fresh locked evaluation data. Version inputs, rubrics and prompts together; replace holdout after any tuning influenced by its results. Publish negative findings, cost and coverage as prominently as wins. Maintain a decision record at each gate with evidence, unresolved risks and the next specifically approved action.
