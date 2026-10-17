---
name: ape-lab
description: Design a controlled synthetic Evaluape experiment when baseline fairness, causal tests, leakage prevention, budgets, or stopping rules need planning; does not execute experiments.
---

# Ape Lab: design a discriminating experiment

Read [evaluation strategy](../../../docs/EVALUATION-STRATEGY.md) and relevant [requirements](../../../docs/REQUIREMENTS.md). Retain their approved-versus-proposed distinction; numeric targets are proposals, not measured guarantees.

- Define a falsifiable hypothesis and counter-hypothesis, unit of analysis, outcome, baseline, intervention, restoration and known confounders. Bundled changes cannot isolate individual contributions.
- Start with deterministic checks; compare the structured method with a strong equal-budget general investigator and a deterministic baseline. Keep model assistance optional and provider-neutral.
- Use fresh synthetic cases. Separate observable inputs from access-controlled scoring oracles; split by incident/template/causal lineage before variants. Public examples cannot serve as hidden holdout. Preserve all attempts and negative outcomes.
- Freeze versions, evidence access, metrics, denominators, uncertainty method, exclusions and stopping rules before execution. Include no-network isolation, resource limits, cancellation, total spend and accounting across retries/agents. Seeds do not guarantee hosted-model determinism.
- Require actual approved baseline/intervention/restoration observations for experimental causal support. Tabletop outcomes check the protocol only; no fabricated replay results or production-causality claims.

Deliver a protocol with unresolved choices, stop/pivot criteria and an approval checklist: architecture/MVP build scope, reviewer, execution scope, provider/data handling and total spending ceiling. Pause at that gate. No code, dependency installation, model calls, real data, infrastructure or production access is authorized by this skill or its invocation; follow [AGENTS.md](../../../AGENTS.md).
