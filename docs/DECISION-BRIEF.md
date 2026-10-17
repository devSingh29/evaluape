# Evaluape: planning decision brief

**Planning / Pre-Alpha — 17 October 2026.** Public repository under `devSingh29/evaluape` is authorized. Architecture, MVP implementation and experimental execution remain unapproved. No product, replay engine, deployment or live integration has been built.

## Recommendation

Start with an **offline, file-first complaint investigator** that accepts a synthetic evidence bundle and produces a reviewable diagnosis, proposed owner/component, actionable issue and regression case. Its first approved technical experiment must actually run isolated synthetic baseline/intervention/restoration replays. Merely asking a model to classify a complaint or proposing tests does not demonstrate the differentiation.

Use **substantiated / unsupported / unresolved** dispositions. Unsupported requires adequate evidence contradicting the specific claim; missing or conflicting evidence is unresolved. A real failure can still have an unknown cause. Intervention results support a bounded explanation in the replay setting, not universal causal certainty.

## Competitive verdict

The broad idea is already occupied. [LangSmith Engine v2](https://www.langchain.com/blog/langsmith-engine-v2-redteam) describes reproduction and iterative testing, with feature-specific private-beta limitations. [Braintrust](https://www.braintrust.dev/blog/active-observability-loop-patterns-debugger) describes hypothesis testing, counterexamples, evidence and approvals. [Raindrop](https://docs.raindrop.ai/simulate/) advertises stateful replay in early access. Langfuse, Phoenix, Promptfoo and DeepEval already supply valuable tracing, experiments and evaluation building blocks.

The hypothesis worth testing is **portable, auditable adjudication and experimental diagnosis that works alongside an existing stack and reduces mistaken conclusions**. Public documentation does not prove that competitors cannot do this. If a strong equal-budget general-model investigator achieves equivalent results, narrow Evaluape to a useful evidence/export tool or stop expanding the platform. See [COMPETITORS.md](COMPETITORS.md) for the sourced comparison and availability caveats.

## Architecture and provisional stack

| Option | Benefit | Main trade-off | Recommendation |
|---|---|---|---|
| Offline CLI, local files | Small install and privacy surface; simple synthetic demo | Manual imports and limited collaboration | First experiment and V0 |
| Modular service plus isolated workers | Shared review, durable jobs and centralized controls | Operational/security overhead | Only after validated demand |
| Distributed workflow platform | Long-lived workflows and independent scaling | Integration and reliability complexity | Defer |

Provisional V0 choice: **Python, versioned JSON bundles and local files**, with SQLite only if persistent querying warrants it. Python is a proposal because of its evaluation ecosystem; TypeScript is viable if maintainer familiarity and adapter demand favor it. No mandatory AI provider, graph database, queue, web framework or hosted service. Future collaborative operation could use PostgreSQL and object storage behind adapters. These choices remain reversible and require approval; no dependencies were installed.

## Smallest differentiated MVP

1. Import feedback, expected behavior and versioned evidence; record missingness.
2. Run deterministic checks and adjudicate the specific claim.
3. Compare a small set of hypotheses using bounded, isolated synthetic replays.
4. Produce evidence-linked findings, limitations and a proposed owning component.
5. Export a reviewable issue and regression case; humans approve consequential use.

Defer autonomous fixes/merges, production replay, live Almic connections, hosted dashboards, broad observability, automatic issue publication and many adapters. Almic is a future design partner, not a dependency or source of public implementations.

## First experiment to approve

Run a **24-case development feasibility study** across the six scenario families, with fresh synthetic cases and separately controlled oracles. Compare deterministic checks, a strong LLM-only investigator with the same tools/budget, and Evaluape's structured method. Include wrong complaints, missing evidence and application bugs blamed on models. Actually execute seeded-fault baseline/intervention/restoration paths in isolation; record all costs and failures. This small study establishes feasibility, not superiority.

If feasible, freeze the protocol and use a fresh powered holdout, initially designed around 240 independent base incidents. Proposed gates include an eight-point macro-F1 uplift with a positive paired confidence bound, useful coverage, false-accusation upper confidence bound at most 10%, and equal-budget accounting. All are targets, not measured results. See [EVALUATION-STRATEGY.md](EVALUATION-STRATEGY.md) for denominators, uncertainty, regression metrics, leakage controls and stop/pivot rules.

## Decisions requested

- Approve or revise offline/file-first V0 and the six-family experimental scope.
- Approve a provisional language, with Python recommended but not locked.
- Choose MIT or Apache-2.0; Apache-2.0 is recommended for its explicit patent terms, subject to owner review. No LICENSE has been applied.
- Name the experiment reviewer and approve the model/provider, data-processing scope and total spending ceiling before any execution.
- Establish a verified private security-reporting route before accepting external reports or code contributions.

Approving public documentation does not approve any of these execution steps. The phased roadmap and ten planning issues are proposals with explicit gates.
