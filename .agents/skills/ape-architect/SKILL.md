---
name: ape-architect
description: Compare Evaluape architecture and scaling alternatives when a technology, portability, persistence, or operational trade-off requires a planning decision.
---

# Ape Architect: choose the smallest viable design

Read [architecture](../../../docs/ARCHITECTURE.md), [requirements](../../../docs/REQUIREMENTS.md), [MVP](../../../docs/MVP.md) and relevant [open questions](../../../docs/OPEN-QUESTIONS.md).

- Start from the approved scope and unanswered operating constraints, not a preferred stack. Current recommendation is synthetic offline/file-first V0; architecture and implementation remain decision gates.
- Compare viable alternatives against data sensitivity, installation burden, durability, recovery, concurrency, expected load and maintainer effort. State assumptions; do not invent throughput targets or production guarantees.
- Preserve deterministic-first operation and optional models. Keep source, model and destination adapters outside a provider-neutral contract. Show how data and review history remain portable without a mandatory vendor, queue, database server or hosted platform.
- Trace proposed components to requirements. Distinguish local needs from later service/tenant controls. Keep provenance, missingness, substantiated/unsupported/unresolved decisions and causal limitations intact across designs.
- Identify reversible decisions, migration triggers, failure modes and the smallest evidence that would justify extra complexity. Prefer a narrow experiment over speculative distributed infrastructure.

Deliver a concise decision proposal: options, trade-offs, provisional recommendation, rejected options, uncertainties and approvals needed. No technology choice, installation, MVP coding, provisioning, paid work or production access is authorized here. Ask for the missing architecture/MVP decisions before dependent implementation, following [AGENTS.md](../../../AGENTS.md).
