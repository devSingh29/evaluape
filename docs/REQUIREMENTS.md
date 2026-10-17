# Evaluape requirements and acceptance gates

Status: planning specification. Nothing in this document means a service, integration, model workflow or replay engine has been implemented. Requirements describe the intended product; the V0 boundary below deliberately proves a smaller offline protocol first.

## 1. Product objective

Help a maintainer move from a feedback claim to an auditable decision: what happened, whether the claim is supported, what explanations remain plausible, what a controlled test establishes, and what an owner should do next. The output is a reviewable issue and regression package with traceable evidence and honest uncertainty.

The project is independent and general-purpose. It must not require Almic, proprietary internal code, internal traces or any single vendor's platform. Existing observability and evaluation products already offer investigation and experiment workflows; Evaluape claims no unique invention of those capabilities. Its proposed value to test is a portable, deterministic-first adjudication and intervention protocol that can preserve reviewer decisions and causal limitations across source systems.

### Primary users

- Maintainer or incident investigator: identifies original evidence, distinguishes failure from expectation disagreement, tests hypotheses, and prepares a useful next action.
- Reviewer or domain expert: supplies a defensible expectation, challenges unsupported causal claims, and approves consequential outputs.
- Adapter contributor: integrates an authorized source or destination without changing the core investigation model.
- Self-hosting operator: controls data access, retention, execution isolation, spend and recovery.

### Non-goals

Autonomous production fixes; self-granted credentials; automatic deployment; automatic blame assignment; universal correctness judgments; guaranteed deterministic reproduction of hosted models; treating traces as ground truth; replacing the source observability system; training on private evidence; live integration with a named proprietary assistant. No implementation, credentials, accounts, infrastructure or production connection is part of this planning deliverable.

## 2. Recommended V0 and later scope

**V0 is an offline/file-first experiment, not a service platform.** Use only synthetic fixtures in V0. Real or redacted incidents belong to a later, separately authorized pilot. Demonstrate one portable investigation bundle that separates feedback, original evidence, expectation, adjudication, hypotheses, replay design/results, review decisions and issue/regression drafts. Run deterministic checks first. A local fixture replay must have no network or external side effects. The core must work without a mandatory model provider. Optional model assistance and model-based benchmark arms require the separately approved experimental protocol, provider and spending ceiling; production model integrations are deferred.

V0 should include synthetic cases for: a substantiated deterministic failure with intervention evidence; a contradicted claim; insufficient evidence; two plausible competing causes; a nonreproducible/stochastic result; and a malicious instruction embedded in evidence. This is a requirements set for a later implementation, not a claim that these tests currently run.

V0 does not need a database server, queue, web UI, live telemetry ingestion, issue tracker publication, collaborative roles, or multi-tenant hosting. Persist local investigation and review records in the bundle. Represent human approval before an export is considered ready for external publication, while leaving actual publication manual. Multi-tenant security requirements become mandatory before shared hosting; offline V0 must not market itself as meeting them.

Later gates can add read-only adapters, collaboration, optional provider-neutral assistance, bounded external replays, and approval-gated publication. Each needs separate validation and authorization. See [ARCHITECTURE.md](ARCHITECTURE.md) for three viable deployment alternatives and provisional technology options.

## 3. Functional requirements

Priority labels: **Core** means required for the portable investigation protocol; **V0** means demonstrated offline; **Later** means required before the named capability ships.

| ID | Scope | Requirement | Acceptance evidence |
|---|---|---|---|
| F-01 | Core, V0 | Ingest a feedback record and separate distinct claims without treating the wording as trusted instructions | Fixture preserves original report, normalized claims and provenance; embedded commands are inert |
| F-02 | Core, V0 | Link claims to original input/output and available traces, tools, retrieval records and versions | Manifest identifies each available artifact and every missing category; ambiguous run matches remain unresolved |
| F-03 | Core, V0 | Preserve original authorized evidence separately from normalization and redaction | Different digests and lineage for original and derivative; modifying a derived view cannot rewrite source evidence |
| F-04 | Core, V0 | Record explicit expected behavior and its source/version/scope | An unsupported expectation produces unresolved adjudication; reviewer changes create a new revision |
| F-05 | Core, V0 | Run deterministic assertions before optional model assistance | The offline path reaches useful verdicts with no model credentials; check versions and outputs are captured |
| F-06 | Core, V0 | Adjudicate each claim as substantiated, unsupported or unresolved | Labelled fixtures exercise all three; absence of evidence never counts as contradiction |
| F-07 | Core, V0 | Explain verdict with supporting, conflicting and missing evidence | Every factual assertion has an artifact citation or explicit inference label; unknowns are visible |
| F-08 | Core, V0 | Preserve multiple plausible explanations and disconfirming tests | A fixture contains at least two competing causes and does not collapse uncertainty into one narrative |
| F-09 | Core, V0 | Freeze replay baseline, interventions, snapshots, metrics, limits and stopping rules before execution | Plan digest changes if any relevant variable changes; results point to the exact approved plan |
| F-10 | Core, V0 | Compare baseline and intervention outcomes without overstating causality | No identified-cause claim from trace correlation alone; bundled changes cannot be attributed independently |
| F-11 | Core, V0 | Capture nondeterminism and replay fidelity limitations | Nonreproducing case retains all attempts and unknown versions; one pass cannot be presented as a verified fix |
| F-12 | Core, V0 | Suggest grouping while preserving distinct claims and allowing reversal | Similar symptoms with different causes are not silently merged; merge/split record retains original cases |
| F-13 | Core, V0 | Explain priority and proposed owner | Unknown prevalence stays unknown; severity, frequency and evidence quality are separate; owner can remain unassigned |
| F-14 | Core, V0 | Produce actionable issue and regression drafts | Bundle has expected/actual behavior, evidence, competing hypotheses, experiments, limitations, next action, owner proposal and assertions |
| F-15 | Core, V0 | Persist investigation history and review decisions | Close/reopen and changed-evidence fixtures keep prior verdicts and approvals; process restart does not erase them |
| F-16 | Later | Publish only an exactly approved revision to a specified destination | Changed text/destination/permissions invalidate approval; ambiguous timeout triggers reconciliation rather than duplicate send |
| F-17 | Later | Use source/destination adapters behind documented contracts | Two unrelated source fixture formats normalize without vendor-specific fields becoming mandatory core requirements |
| F-18 | Later | Support versioned OpenTelemetry imports with explicit completeness | Adapter records mapping version/schema metadata, span correlation and dropped/missing data; unsupported conventions fail visibly |
| F-19 | Later | Allow optional provider-neutral model assistance | Swap or disable providers without changing core records; output remains a suggestion, citations are validated, no approval can be generated |
| F-20 | Core, V0 | Export/import a portable authorized bundle | Round-trip preserves digests, lineage, limitations and review history; historical approvals do not grant new destination authority |

## 4. Investigation semantics

### Claim validation versus root-cause analysis

A failure claim can be substantiated while its cause remains unresolved. A replay may fail to reproduce a genuine historical failure. Unsupported applies only to a scoped claim with adequate contrary evidence, never to an empty trace or unsuccessful retrieval. A report with multiple claims can have mixed verdicts. Human reviewers may revise decisions, but previous evidence and decisions remain available subject to retention policy.

### Required causal claim guardrail

Observational traces support statements such as “the missing retrieval result is consistent with this failure.” They do not support “retrieval caused this failure” by themselves. Strong causal language requires controlled intervention evidence, recorded baseline, defined outcome, credible fidelity, explicit confounders and scoped conclusions. The approved label is “intervention-supported in this replay setting,” not a universal claim. If those conditions are absent, the system must say the cause is unresolved or a hypothesis.

A counterfactual intervention changes a simulated or reconstructed setting. It does not recreate the unobserved alternate production history. Hidden provider changes, caching, external state, tool nondeterminism, unrecorded prompt transformations, sampling and evaluator variability can all limit inference. A model's self-explanation is not mechanistic evidence.

### Actionable output minimum

1. A concise symptom and affected scenario.
2. Original run/reference and evidence manifest version.
3. Expected behavior, source and applicability.
4. Claim verdict with evidence and uncertainty.
5. Competing hypotheses and why they remain or were disfavored.
6. Replay conditions, intervention, baseline, all attempts, result and limitations, or reason replay was unavailable.
7. Priority rationale and proposed owner, with unknowns preserved.
8. A concrete next action, acceptance criterion, and regression candidate.
9. Privacy/disclosure review and approval status.
10. Distinction between investigation completion, publication, and actual fix verification.

## 5. Safety and privacy requirements

| ID | Requirement | Release gate |
|---|---|---|
| S-01 | Feedback, traces, retrieved text and tool output are untrusted data; no instruction in them grants capability or approval | Malicious fixture cannot execute commands, fetch embedded URLs, change rubric, expose data or publish |
| S-02 | Replay defaults to no network and no side effects outside disposable scratch | Test blocked egress, read-only mounts, absent production credentials and termination of child processes; document isolation limits |
| S-03 | CPU, memory, wall time, process count, output size, attempt count and external spend have hard limits | Exhaustion produces partial/inconclusive result, not hidden retry/escalation; concurrent budget reservations cannot overspend |
| S-04 | Any permitted network/model/tool access is explicit, narrowly scoped and auditable | Changed capability or destination invalidates previous approval; replay runner cannot bypass control-plane policy |
| S-05 | Evidence is redacted before wider sharing or external model use | Secret/PII canary absent from public draft, logs, indexes and exports; derivative lineage preserved |
| S-06 | Retention and deletion apply to evidence and all controlled derivatives | Purge test covers blobs, indexes, caches, fixture exports and documented backup lifecycle; tombstone does not retain prohibited identifiers |
| S-07 | Every shared-hosting object and lookup is tenant-scoped | Cross-tenant ID substitution, search, cache, blob URL, job and duplicate-query tests deny access |
| S-08 | Human approval binds revision, action, target, data, capability, budget and expiry | Stale, revoked, mismatched or forged approvals fail closed; content-derived approvals are rejected |
| S-09 | Executable plugins and replay code are supply-chain risks, not trusted because they are adapters | Pin reviewed artifacts, isolate execution and test malicious adapters; no automatic code install from evidence |
| S-10 | Sensitive access and consequential actions leave non-sensitive audit records | Audit survives retries/restarts; credentials and raw private prompts do not leak into logs |

No-network means enforced execution policy, not an instruction to a model. The exact isolation mechanism is a decision gate. A local prototype that lacks strong hostile-code isolation must only run trusted fixture evaluators and must clearly state that boundary.

## 6. Reliability and operations requirements

- **R-01 Durable progress:** investigations, manifests, plans, attempts, approvals and publications survive process restarts. Recovery cannot silently skip a stage or lose a decision.
- **R-02 Idempotency:** repeated intake does not create duplicate reports; repeated analysis may produce referenced attempts; repeated publication must not create duplicate external issues. Distinguish these identities.
- **R-03 Concurrency:** revision checks prevent stale workers from replacing newer evidence or decisions; leases and fencing prevent duplicate commits after worker recovery.
- **R-04 Partial failure:** represent individual artifact failures, missing snapshots, cancellation, timeout, corrupt output and uncertain external submission distinctly.
- **R-05 Storage integrity:** verify digests when loading evidence; fail to unresolved/blocked on corruption. Hashes are not authenticity claims.
- **R-06 Reproducibility disclosure:** state which versions were pinned, which were aliases, which dependencies are absent, and which results are stochastic.
- **R-07 Observability:** record stage latency, retries, queue age if present, artifact gaps, budget usage, review overrides and publication reconciliation without exposing evidence text.
- **R-08 Recovery testing:** a future service must demonstrate backup/restore, interrupted acquisition, stale approvals, exhausted budgets, and deletion semantics before production use. Recovery targets are selected after deployment needs are known, not asserted here.

V0 should measure local processing time and artifact sizes on declared fixtures. Do not set arbitrary high-throughput promises before representative workloads exist. Later service SLOs require volume/concurrency, data sizes, replay durations and acceptable failure modes from intended operators.

## 7. Evaluation and decision criteria

Use a labelled set reviewed independently of any optional model evaluator. Include genuine failures, mistaken feedback, incomplete traces, ambiguous expectations, malicious text, stochastic outputs, interacting causes, false duplicate candidates and unavailable historical versions. Report sample counts and uncertainty; do not advertise accuracy from a tiny synthetic suite.

Measure:

- Claim verdict agreement and especially false substantiation/false rejection rates.
- Correct abstention when evidence or expectations are inadequate.
- Evidence citation validity and completeness of recorded gaps.
- Unsupported causal-claim rate; this is a release-blocking safety metric when an output overclaims.
- Replay plan fidelity and whether intervention conclusions match the known synthetic mechanism.
- False merges/splits and reversibility of dedup decisions.
- Regression usefulness: catches the intended failure, passes an approved repaired variant, and does not overfit a single answer string.
- Reviewer time to an actionable decision and number/reasons of overrides.
- Isolation, approval bypass, privacy leakage, restart recovery and budget-limit test results.

Before scoring, agree acceptance thresholds and failure costs with intended users. Start with a go/no-go review of the protocol: does it preserve distinctions ordinary issue text loses, and can another tool consume it without the original vendor? If not, revise the product hypothesis before adding a service stack.

## 8. Open questions and decision owners

| Question | Needed before | Owner |
|---|---|---|
| Which initial user and feedback domain provides a useful, non-proprietary test? | V0 fixture design | Product maintainer |
| What constitutes a sufficiently specific expectation in that domain? | Adjudication rubric | Domain reviewer |
| Which portable format and schema-version policy should be public? | First implementation | Maintainer + adapter contributor |
| Which language matches contributor skills and offline deployment needs? | Implementation | Maintainer |
| Can trusted fixtures prove value before any external integration? | V0 scope approval | Product maintainer |
| Which isolation boundary meets the intended threat model? | Any untrusted replay | Security reviewer/operator |
| What private evidence may be retained or sent to model providers? | Real evidence or optional assistance | Data owner/operator |
| Are shared hosting and multi-user approvals necessary? | Architecture B/C selection | Operator + maintainer |
| Which metric, sample size and budget support stochastic comparisons? | Stochastic replay | Evaluation reviewer |
| What constitutes a consequential change and who may approve it? | Publication or mutating integration | Workspace owner |

## 9. Source and compatibility note

OpenTelemetry support is an interoperability target, not an assertion that every trace captures enough evidence to reproduce a run. Official [semantic-convention documentation](https://opentelemetry.io/docs/specs/semconv/) and the [GenAI landing page](https://opentelemetry.io/docs/specs/semconv/gen-ai/) were checked on 2026-10-17 and point GenAI conventions to a separate repository. Implementation must pin and reverify its mapping revision. See the architecture document for the security source and exact compatibility policy. No dependency versions or vendor-specific live integrations are committed in this plan.
