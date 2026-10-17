# Prioritized planning backlog

These are proposed issue bodies, not created GitHub issues, assigned work, or permission to execute the MVP. Public repository ownership is decided: `devSingh29/evaluape`. Priorities express recommended sequencing, not committed dates. The owner must approve implementation and external actions separately.

## Planning label manifest

The ten labels below have been created at [devSingh29/evaluape/labels](https://github.com/devSingh29/evaluape/labels). Existing default labels were preserved.

| Label | Meaning | Suggested color |
| --- | --- | --- |
| `planning` | Research or specification, no implementation | `5319E7` |
| `decision-needed` | Owner choice required | `FBCA04` |
| `P0` | Resolve before dependent planning or execution | `B60205` |
| `P1` | Next planning work | `D93F0B` |
| `P2` | Later planning refinement | `0E8A16` |
| `evidence` | Case provenance, hypothesis support, or oracle boundaries | `1D76DB` |
| `evaluation` | Baselines, metrics, protocols, or scoring | `0052CC` |
| `privacy-security` | Sensitive-data and security boundaries | `D4C5F9` |
| `research` | Source-supported competitive or user research | `C2E0C6` |
| `blocked-approval` | Cannot proceed without explicit scoped approval | `E4E669` |

## 01 — Finalize licensing and publication readiness

**Priority/labels:** P0 · planning · decision-needed · blocked-approval

**Outcome:** Record the approved public destination `devSingh29/evaluape`, resolve license choice and copyright holder, and check all artifacts for public sharing.

**Acceptance criteria:** Ownership/publication approval is recorded; LICENSE remains absent until separately approved; no private data or Almic assets are published; private security contact setup is assigned before accepting external contributions.

**Dependencies/approvals:** Public repository creation and publication at the approved destination are authorized and handled by the coordinating maintainer. License application still requires owner approval; do not independently duplicate remote actions.

## 02 — Define the target diagnostic job

**Priority/labels:** P0 · planning · research

**Outcome:** Choose a primary engineer persona, one failure-investigation workflow, and a clearly bounded problem statement.

**Acceptance criteria:** Document current alternatives, evidence for the problem, unvalidated assumptions, and conditions under which Evaluape is unnecessary. Specify what useful output looks like to that user.

**Dependencies/approvals:** Owner review; any user interviews or external outreach need separately authorized recipients and purpose.

## 03 — Validate competitive assumptions

**Priority/labels:** P0 · planning · research

**Outcome:** Compare the proposed workflow with current LangSmith Engine, Raindrop, Braintrust, and Arize AX capabilities.

**Acceptance criteria:** Cite primary sources and review dates; distinguish documented, observed, unknown, and proposed capabilities; identify baseline candidates and falsifying counterexamples; avoid unsupported uniqueness claims.

**Dependencies/approvals:** Issue 02 informs relevance. Read-only research only; vendor account creation or trials are not authorized.

## 04 — Specify the diagnostic evidence contract

**Priority/labels:** P0 · planning · evidence

**Outcome:** Describe portable evidence IDs, provenance, ordering, missingness, hypothesis citations, and uncertainty.

**Acceptance criteria:** Contract distinguishes observations from interpretations; includes an inconclusive outcome; explains optional provider adapters; makes no mandatory provider-specific fields; reconciles with DATA-MODEL.md.

**Dependencies/approvals:** Issue 02. Approval required before implementing parsers or integrations.

## 05 — Curate synthetic diagnostic cases and oracle boundaries

**Priority/labels:** P0 · planning · evidence · evaluation

**Outcome:** Review a small, intentionally varied synthetic case set and its separate evaluation-only answer material.

**Acceptance criteria:** Every case meets CONTRIBUTING.md's checklist; observable evidence excludes hidden fault labels and intervention answers; include ambiguous and insufficient-evidence cases; document case-author clues and leakage risks; cover competing causes rather than only obvious faults.

**Dependencies/approvals:** Issue 04; synthetic authoring only. No live or redacted real traces.

## 06 — Pre-register the comparison protocol

**Priority/labels:** P0 · planning · evaluation · decision-needed

**Outcome:** Propose credible baselines, scoring rules, cost and effort measures, repeated-trial handling, and failure thresholds before any run.

**Acceptance criteria:** State hypothesis, case splits, oracle access, blinded review where feasible, uncertainty handling, intervention controls, reproducibility limits, and numerical go/no-go thresholds for owner approval. Define a stop condition and prohibit changing thresholds after observing results without recording the change.

**Dependencies/approvals:** Issues 03–05. Protocol review is not authorization to run models or spend money.

## 07 — Review privacy and threat model

**Priority/labels:** P1 · planning · privacy-security

**Outcome:** Identify threats arising from traces, imports, exports, prompt injection, model calls, and future integrations.

**Acceptance criteria:** Map trust boundaries and data flows; distinguish proposed controls from implemented ones; require synthetic-only initial experiments; document retention/deletion expectations; establish an approved private reporting route before accepting external security reports or code contributions.

**Dependencies/approvals:** Issue 04. No penetration testing, credential handling, or security-setting changes.

## 08 — Review architecture and scope exclusions

**Priority/labels:** P1 · planning · decision-needed

**Outcome:** Check that the proposed architecture serves the research question without becoming an observability platform.

**Acceptance criteria:** Identify minimal components and optional adapters, unresolved language/storage choices, non-goals, portability trade-offs, and deferred work; reconcile architecture, requirements, MVP proposal, and roadmap.

**Dependencies/approvals:** Issues 02, 04, and 06. No dependency installation, build system, CI, deployment, or application implementation.

## 09 — Request a bounded technical experiment

**Priority/labels:** P1 · planning · blocked-approval · evaluation

**Outcome:** Prepare a decision packet for a possible future spike, not the spike itself.

**Acceptance criteria:** Packet names exact deliverables, branch `codex/<task-name>`, cases, allowed tools/providers, cost cap, data-transmission scope, runtime budget, success/failure thresholds, stop condition, and reviewer. Explicit architecture and MVP approval, together with scoped experiment approval, is recorded before code or external execution.

**Dependencies/approvals:** Issues 01 and 04–08. Owner may reject or narrow the experiment. This backlog does not approve it.

## 10 — Design the post-experiment decision review

**Priority/labels:** P2 · planning · evaluation

**Outcome:** Define how a future result will support stop, revise, or continue decisions.

**Acceptance criteria:** Review template compares results against pre-registered thresholds and baselines, includes negative findings, failure cases and costs, records deviations and limitations, and treats inconclusive evidence honestly. Further implementation requires a new approval rather than automatic MVP execution.

**Dependencies/approvals:** Issue 06 defines the protocol. Do not fabricate results; an actual review waits for an approved, completed experiment.
