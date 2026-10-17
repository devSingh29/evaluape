# Evaluape evaluation strategy

Status: planning only. No experiment, installation, model call, instrumentation, or implementation is authorized by this document. All numbers below are proposed, aspirational decision thresholds, not measured results.

## Hypothesis and counter-hypothesis

Given an AI complaint plus the same available evidence and resource budget, structured adjudication with discriminating interventions produces more correct, evidence-substantiated diagnoses and fewer false accusations than a competent LLM-only investigator. The useful output is an actionable engineering issue and a discriminating regression case, including an explicit “cannot determine” when appropriate.

The counter-hypothesis is that a good general LLM with the same trace, tools, and budget does just as well. Trace → eval → fix is already represented in products such as LangSmith Engine and Raindrop Workshop; that sequence alone is not differentiation. This experiment tests incremental diagnostic value, not whether incident summaries can be generated. Competitive assertions require separate source verification before publication.

## What is being judged

Separate four questions; success on one does not imply success on the others:

1. **Complaint adjudication:** `substantiated`, `unsupported`, or `unresolved` for a precisely stated claim and its declared scope. A correct response may be poorly presented; an incident can be real while the user's proposed cause is wrong. Missing evidence is not proof of a false complaint. Here `unsupported` means the observed claim is contradicted by adequate evidence under the stated contract; absence of adequate evidence is `unresolved`.
2. **Localization:** ranked component hypotheses, including retrieval/ranking, knowledge coverage/freshness, model reasoning, schema/serialization, application logic, and no established defect. Multi-causal cases can have several valid locations. Do not conflate trigger, contributing factor, and root cause.
3. **Causal support:** a diagnosis substantiated only by correlation is weaker than a controlled intervention with a matching observation. Synthetic generator truth is a scoring oracle, not investigator evidence.
4. **Regression quality:** a case that catches the observed defect and passes the minimally corrected behavior without overfitting to wording or the proposed fix.

Output contract: claim and scope; adjudication probabilities; verdict/abstention; evidence citations; missing evidence; ranked hypotheses with contradicted alternatives; intervention proposal and result if available; reproduction level; issue with owner/component, impact and acceptance criteria; regression case with input, expected behavior, and justification. Never invent executed tests or an available reproduction environment.

## Dataset and leakage boundaries

Six scenario families are required: wrong retrieved context; missing or outdated knowledge; unsupported complaints; model reasoning mistakes; schema mapping failures; application bugs blamed on the LLM. Every family needs realistic distractors and matched alternatives. Include ambiguous, multi-causal, insufficient-evidence, and non-reproducible cases; unsupported complaints must not become an easy linguistic tell.

Use invented generic environmental inspections only for the initial illustrations. No Almic data, prompts, code, customer details, or implementation are permitted. Later cross-domain examples must be independently authored. All example facts, rules, and thresholds are fictional and not environmental or regulatory advice.

Each case has a stable opaque ID and two separately stored records:

- **Observable:** complaint, task contract, versioned source excerpts, model/input/output trace, app behavior, chronology, permissions and missing artifacts. It must contain only what an investigator could have observed. Neutral filenames and no root-cause, split, label, or intervention-result hints in titles or IDs.
- **Private oracle:** causal construction, adjudication target, admissible hypotheses, hidden fault, expected counterfactual outcomes, scoring notes, and split metadata. This file is available only to benchmark construction/scoring, never the investigator, its tools, prompts, retrieval index, or citations. “Private” in this planning repository is a logical role, not an access-control claim; the illustrative oracle is readable by repository readers and is unsuitable as a hidden test.

The bundled nine fixtures are public design illustrations, not benchmark or training data and not evidence of efficacy. Do not reuse them in scored holdout. For an approved study, create fresh cases, strip construction metadata from investigator payloads, freeze hash manifests, and use separate access-controlled scoring storage. Investigator sessions must lack repository/oracle access, rather than merely being told not to read it. Check logs for leaked labels, compare observable fields for accidental answer tokens, and have an independent reviewer judge plausibility and leakage. Test whether a classifier can infer labels from length, IDs, formatting, or complaint vocabulary alone.

Split by **scenario-generation family/template, causal mechanism variant, entity/source set, and paraphrase lineage** before generating variants. High-level categories can occur in all splits, but no base incident or mechanically equivalent template crosses splits. Maintain an overlap audit and record provenance. Suggested development set: 60 training cases for format/examples, 60 dev cases for thresholds and protocol choices, and 240 locked held-out base incidents (40 per high-level family). Add paired healthy/faulted variants within the same split; analyze them as a cluster, not independent observations. Target at least 30% ambiguous, unsupported, multi-causal, or insufficient-evidence incidents overall and meaningful representation in each category. Balance adjudication labels deliberately; record sampling weights and a separate realistic-prevalence analysis.

Two independent domain-informed reviewers label each case without seeing a system's output; a third resolves disagreements. Record agreement and disputed judgments. An ambiguous oracle should permit multiple diagnoses or require abstention; do not manufacture single-label certainty. Reviewers grading outputs are blinded to system identity. Oracle construction and output scoring should use different people where feasible.

## Comparators and fair budget

Freeze model/provider/version, temperature policy, permitted evidence, tool descriptions, token accounting, context limits, retrieval corpus, and intervention costs before holdout. Every arm receives the same initial observable record and access to the same read-only evidence and isolated synthetic intervention catalog. For the technical experiment, an isolated synthetic replay harness must actually run seeded-fault baseline, intervention and restoration paths after approval. It returns observed traces and outputs, never oracle explanations. Pre-authored expected outcomes are scoring references only. Equal-budget arms receive the same harness capabilities. Tabletop or simulated-only outcomes can validate the output contract but cannot validate experimental root-cause diagnosis.

1. **LLM-only baseline:** a strong investigator prompt developed on dev, instructed to assess evidence, consider alternatives, abstain, propose tests, and produce the same output contract. It has the same tools, model, context and total budget as Evaluape, but no prescribed Evaluape stages/state.
2. **Deterministic baseline:** fixed schema checks, exact source/version matching, arithmetic checks and contract assertions. Reports unresolved outside its scope. Freeze all rules before holdout. Record actual lower cost; it need not waste tokens to match the budget.
3. **Evaluape hypothesis:** structured claim/evidence graph, competing explanations, explicit uncertainty, and selection of a discriminating intervention before a causal conclusion.
4. **Ablations:** remove interventions; remove competing hypotheses; remove evidence provenance checks; remove calibrated abstention. Use the same total cap, allowing remaining stages to use freed budget, and report actual usage. Also compare Evaluape without scaffolding against the LLM-only prompt to isolate prompt-quality effects.

Proposed per-case budget: at most 12,000 aggregate input/output tokens, six evidence/tool calls and two interventions, with a 180-second wall-clock ceiling. Count retries and every model in a multi-agent path. Set a USD cap after selecting the model and current prices, before approval; do not treat token parity as dollar parity across different models. No paid calls until the full study spending ceiling is approved. Run arms on identical cases in randomized order; preserve failures and timeout outcomes. A second model family is a generalization check, not a replacement for a failed primary comparison.

## Metrics and uncertainty

| Metric | Definition | Aspirational target on locked holdout |
| --- | --- | --- |
| Adjudication | Macro F1 across substantiated/unsupported/unresolved; per-class precision/recall and full confusion matrix | ≥0.80 and ≥0.08 absolute over LLM-only |
| Abstention and coverage | Resolved coverage versus adjudication error among resolved cases; risk–coverage curve, classwise reliability, multiclass Brier score and ECE with bins frozen on dev | ≥70% resolved coverage at ≤10% error; ECE ≤0.08, with bootstrap CI |
| Localization | Top-1 and top-3 component accuracy on identifiable single-cause cases; set precision/recall/F1 for multi-causal cases | Top-1 ≥0.75 and ≥0.10 above LLM-only; multi-cause set F1 ≥0.70 |
| Intervention support | Fraction of causal claims with a discriminating test whose observed result supports the claim and rules out at least one live alternative; blinded validity rubric | ≥80% of asserted causal diagnoses substantiated; report untestable cases separately |
| False accusations | Unsupported claims that a component, model, source, or person is responsible, divided by all causal assertions; separately report incident-level rate and unsupported-complaint subgroup | ≤5%; do not hide zero-claim systems behind this metric |
| Reproducibility | R0: narrative only; R1: evidence replay; R2: deterministic replay reproduces symptom; R3: controlled intervention removes symptom and restoration reintroduces it | ≥80% correctly assign level; ≥70% of replay-eligible confirmed defects reach R2+ |
| Regression sensitivity | Faulted variants caught / all faulted variants, clustered by base incident | ≥85% |
| Regression specificity | Healthy variants passed / all healthy variants | ≥90% |
| Cost and latency | All-arm tokens, model/tool USD, interventions, retries, p50/p95 latency and timeout rate | Within equal caps; ≥0.08 F1 gain without >1.5× baseline median actual cost |
| Issue usefulness | Blinded engineer rates evidence traceability, component routing and testable acceptance criteria on 1–5 scale; record time to understand/act | Median ≥4; exploratory, not a substitute for correctness |

Require citation validity and no invented results as separate hard checks. Report causal claims per case, coverage, and issue yield alongside accusation rate so indiscriminate abstention cannot win. Substantiated/unsupported/unresolved are ground-truth adjudication labels; operational abstention is an action, not automatically a correct unresolved label. Score both explicitly. Probability calibration applies to adjudication and separately to localization if confidence is emitted.

Use paired, case-cluster bootstrap 95% confidence intervals for score differences and F1; Wilson intervals for simple independent proportions; cluster bootstrap when variants or repeated runs are present. Include full counts and denominators. At n=240 independent incidents, a proportion near 50% has approximately ±6.3 percentage-point 95% uncertainty; at n=40 per family, approximately ±15.5 points. Subgroup conclusions therefore remain exploratory. A measured 5% accusation rate among only 100 assertions has a wide interval and does not establish a strict 5% upper bound. Specify a target of upper 95% bound ≤10% for that safety gate and report actual precision. Do not advertise the aspirational point targets as established guarantees.

Pre-register macro-F1 uplift as the primary endpoint. Use paired dev variance to simulate power for an eight-point difference and choose the final holdout size before unblinding; 240 is a starting design, not a power guarantee. If budget cannot support adequate power, label the study exploratory and do not claim superiority. Keep secondary metrics descriptive or apply a declared multiplicity correction. Repeated stochastic runs (suggested three on 30 preselected incidents) assess stability, not additional independent sample size.

## First experiment protocol, awaiting approval

1. Approve scope, model, data handling, intervention safety, maximum spend and human-review effort. Keep all execution synthetic and isolated; no customer source access or live modifications.
2. Author fresh train/dev cases and validate six families plus negatives. Human-review leakage, internal consistency and causal identifiability. After separate build/execution approval, implement only the isolated synthetic seeded-fault replay needed for the study; record baseline, single-factor or factorial intervention, and fault-restoration observations with versions/seeds. Lock rubrics and oracle expectations independently from actual outcomes. Do not reinterpret an unexpected replay result to match the oracle.
3. On 24 dev incidents, test feasibility and equal-budget baseline quality. No efficacy claim. Stop if >10% invalid fixtures, any oracle exposure, invented intervention execution, or a material budget/accounting discrepancy. Repair and repeat dev only.
4. Tune on remaining dev data; freeze prompts, rules, confidence thresholds, scoring, dataset manifests, model settings and budget. Estimate required holdout size. Register hypotheses and exclusion policy. No exclusions for difficult-but-valid cases.
5. Run all frozen arms on locked holdout only after explicit execution approval. Execute bounded synthetic controlled replays, including baseline/intervention/restoration for identifiable faults and factorial tests for multi-cause cases. Capture evidence access, outputs, costs, timeouts and actual intervention results. If only proposed or pre-authored outcomes are available, stop short of a causal-validation claim. Blinded reviewers score; resolve disagreements without exposing system identity.
6. Report raw counts, per-family failures, paired intervals, calibration/coverage and costs. Publish a redacted example bundle with oracle separated only after scoring is final. Any post-holdout design change requires a new untouched holdout.

### Stop, proceed, and pivot gates

- **Immediate stop:** oracle leakage, fabricated evidence/test execution, sensitive real data ingestion, unsafe external mutations, or exceeded authorized spend. Preserve audit evidence; repair only in dev and replace compromised holdout.
- **Proceed to a small human-reviewed pilot:** primary uplift point estimate ≥0.08 with 95% paired CI lower bound >0, all budget/citation hard checks pass, and false-accusation upper 95% bound ≤10% with useful coverage. Localization and regression targets must be directionally met; disclose any miss and limit pilot scope accordingly.
- **Inconclusive:** uplift CI crosses zero or sample is underpowered. Report uncertainty. Obtain approval for more independent cases or a narrower hypothesis; do not repeatedly peek or add samples until significance appears.
- **Pivot to a lightweight evidence/issue exporter:** no meaningful uplift over a well-tuned LLM-only baseline, or benefits disappear with equal budgets. Preserve useful workflow artifacts without claiming a diagnostic engine.
- **Pivot to a narrow deterministic wedge:** repeatable benefit appears only in schema, version or contract checks. Validate that subset with fresh cases and a stronger deterministic baseline.
- **Do not advance autonomous fixing:** even strong synthetic results establish neither production reliability nor authorization for code changes. Human-reviewed external validation is a separate gate.
