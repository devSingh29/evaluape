# Smallest useful MVP

Status: proposal only. No executable implementation, deployment, installation or experiment is included.

## User and job

For the engineer who receives “the AI gave the wrong answer,” turn one complaint into a substantiated verdict, a bounded causal investigation, and a useful issue/regression specification. The user should be able to see what is known, what is missing, and what would distinguish competing explanations. Success is incremental correctness versus an equally resourced LLM-only investigation, not a polished summary.

## One narrow loop

**Feedback → evidence → investigation → diagnosis → actionable issue → regression case.**

1. Intake one complaint and explicit acceptance contract. Capture what the user claims happened, what output they expected, and whether the claim concerns model output or application behavior.
2. Attach a small versioned evidence bundle: source excerpts, retrieval candidates, selected context, model request/response, schema and displayed/stored result. Mark absent evidence instead of filling gaps.
3. Adjudicate substantiated/unsupported/unresolved; state probabilities and a concise evidence-linked rationale.
4. Rank a few component hypotheses. Choose the cheapest permitted intervention capable of distinguishing live alternatives. The approved technical V0 must actually execute bounded, isolated synthetic seeded-fault baseline/intervention/restoration replays. Human review governs any later real-incident intervention. Proposed or pre-authored outcomes alone do not validate experimental root-cause diagnosis. No replay harness is implemented or run in this planning deliverable.
5. Produce a diagnosis with explicit confidence, alternatives, missing data and reproduction level. Abstain where the causal link is unestablished.
6. Export a reviewable issue and regression specification. The issue cites observed evidence, impact, likely owning component, acceptance criteria and one next action. The regression specifies task input, required evidence/version, intended outcome and the paired healthy/faulted check. A human decides whether to file or execute it.

## Minimum interface and artifacts

A proposed offline, file-first CLI plus reviewable Markdown/JSON outputs is sufficient for V0; no service infrastructure is required. Input and output schemas should be documented before implementation. No hosted dashboard is needed. The artifact should preserve hashes/versions and provenance without exposing secrets. A case ID must connect the complaint, evidence, hypotheses, tests and issue.

Suggested review states: received, evidence incomplete, investigated, review required, exported. A status is not a claim that a test ran. Clear `proposed` versus `observed` intervention records are mandatory. Cross-platform means a neutral export contract first, not six integrations.

## Acceptance criteria

- Handles the six families and ambiguity/multi-cause/missing-evidence negatives in EVALUATION-STRATEGY.md.
- Every factual assertion points to observable evidence; no oracle input, unsupported blame or invented execution.
- Can return a useful unresolved result specifying the smallest missing artifact or discriminating test.
- Produces an issue an engineer can triage and a regression spec that differentiates faulty from healthy behavior.
- Complete evidence access and resource accounting permits a fair baseline comparison.
- Actual approved synthetic replay records show what changed under a bounded intervention and whether restoring the seeded fault restores the symptom. Separate intended outcomes from observations and abstain when replay is inconclusive.
- Demonstrates the pre-registered diagnostic uplift and safety gates before expanding scope. Nine authored examples are a format check, not acceptance evidence.

## Explicitly deferred

Autonomous fixes, patch generation as a core promise, merges, production reruns, write-access integrations, automatic issue submission, dashboard analytics, full observability, broad tracing infrastructure, agent orchestration platforms, continuous monitors, training/fine-tuning pipelines and enterprise administration. Established observability products remain sources of traces rather than systems to replace.

## Adoption and installation plan, not an installation

1. Interview three to five engineers using existing trace tools; have them walk through recent anonymized complaints and quantify investigation effort. Obtain permission before handling any real data.
2. Start with manual, user-approved export of a single redacted incident; accept platform-neutral JSON and text rather than requiring SDK installation or production instrumentation.
3. Review the output alongside the existing investigator workflow. Measure correctness, time to a useful issue, evidence gaps, and repeat use. Do not require a workflow migration.
4. If the synthetic and human-reviewed gates pass, propose a separately approved read-only connector for the most common trace source. Document least privilege, retention, deletion, local/hosted processing and model-provider data exposure before setup.
5. Only then package a versioned installer with dependency inventory and uninstall instructions. No package, credentials, permissions, subscriptions, or integrations are created by this plan.

Adoption stop signal: users cannot supply the needed evidence, outputs merely restate existing trace-tool results, or review cost exceeds saved investigation effort. Narrow the problem or stop before building additional connectors.
