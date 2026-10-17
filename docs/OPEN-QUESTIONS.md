# Open questions and decision gates

Planning work and a public repository under `devSingh29/evaluape` are approved, and the default branch is `main`. Feature implementation must wait for explicit approval of the architecture and MVP. The remaining questions below do not reopen those instructions. Document proposals are not approvals.

| Decision | Why it matters | Needed before |
| --- | --- | --- |
| MIT or Apache-2.0, and who is the copyright holder? | Intended openness is not a license grant. | Adding LICENSE or accepting public contributions |
| Which engineer persona and failure workflow are primary? | Prevents a broad observability platform from replacing a focused question. | Finalizing experiment scope |
| Which concrete failure classes are in the first experiment? | Determines fixtures, observability, and oracle rules. | Case freeze |
| What baseline represents current practice? | Improvements must beat a credible alternative. | Experiment approval |
| What constitutes a supported diagnosis versus an inconclusive result? | Avoids equating confidence or fluent text with correctness. | Scoring rubric approval |
| Which inputs are observable and which are evaluation-only? | Controls oracle leakage and permits fair comparisons. | Fixture and harness approval |
| How are intervention effects separated from stochastic variance? | A changed outcome alone does not prove a cause. | Experiment approval |
| What budgets, model providers, external calls, and dependencies are permitted? | Experiments may incur cost and transmit data. | Any installation or external execution |
| What numerical success, failure, and stop thresholds will be used? | Prevents post-hoc goal changes. | First measured run |
| What is the minimum portable contract, and which adapters are optional? | Preserves portability without prematurely standardizing everything. | Implementation approval |
| Who maintains the project and receives private security reports? | No inbox or reporting feature is currently established. | External contributions or release |

## Approval sequence

1. Complete the approved planning work and collect feedback on the problem and intended user.
2. Carry out the approved public repository decision under `devSingh29/evaluape`; decide the license and copyright-holder details independently of implementation.
3. Obtain explicit approval of the architecture and MVP, plus a specific experimental protocol: cases, evidence boundaries, baselines, metrics, thresholds, budget, providers, and stop condition.
4. Only then approve a bounded technical spike on a named `codex/` branch.
5. Review results and decide whether to stop, revise, or authorize further work.

No step implicitly approves the next. Record actual decisions with date, approving owner, scope, and a reference to the approval. Do not fabricate completed decisions or commit an inferred author identity.

## Recorded owner decision

On 2026-10-17, the owner requested “Public repo under devsingh”; the coordinating maintainer resolved this to the verified account and destination `devSingh29/evaluape`. This supersedes the earlier private-planning direction. It does not approve implementation or choose a license.
