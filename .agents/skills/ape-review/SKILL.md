---
name: ape-review
description: Review Evaluape planning readiness or proposed regression coverage when a decision packet, issue draft, or release-gate assessment needs independent scrutiny.
---

# Ape Review: check readiness and regression claims

Use the relevant [requirements](../../../docs/REQUIREMENTS.md), [MVP criteria](../../../docs/MVP.md), [evaluation strategy](../../../docs/EVALUATION-STRATEGY.md) and [decision brief](../../../docs/DECISION-BRIEF.md). Review only the requested scope; do not invoke every other skill by default.

- Trace each claimed capability or conclusion to an artifact, citation or actual observation. Separate proposals, authored examples, executed results and validated outcomes. Missing proof stays missing.
- Check that deterministic-first operation, provider neutrality and synthetic-only V0 survive the proposed change. Reject live/private Almic dependencies and oracle leakage into investigator evidence.
- Verify substantiated/unsupported/unresolved semantics and separate evidence from causal attribution. A single passing replay is not a verified fix; require the planned observations, limitations and all failed attempts.
- For a proposed regression, identify the faulted behavior it catches, healthy behavior it preserves, required versions/evidence, and why assertions do not merely encode wording or oracle labels. Assess missing-evidence, multi-cause, stochastic and hostile-input negatives where relevant.
- Check readiness against explicit human decisions: architecture/MVP, experimental scope, spend, privacy and any production or publication authority. A favorable review cannot supply those approvals.

Deliver findings ordered by consequence, evidence locations, proposed repairs, and a scoped disposition: ready for human decision, needs revision, or blocked. State untested assumptions and remaining approval owners. Do not implement fixes, execute experiments, publish issues or declare a production release; follow [AGENTS.md](../../../AGENTS.md).
