# Evaluape

<p align="center"><img src="assets/evaluape-logo.png" alt="Evaluape realistic ape portrait" width="180" /></p>

**Planning / Pre-Alpha · Public planning repository · Intended open source**

Evaluape is a proposed, independent project for evidence-based diagnosis of failures in AI applications. It is independent of Almic. There is no installed product, runnable application, released package, or implemented MVP in this repository.

The working hypothesis is that a portable diagnostic workflow can help an engineer move from an observed failure to competing explanations, a discriminating experiment, and a measured fix. A plausible explanation is not a verified cause. Evidence, uncertainty, and inconclusive outcomes must stay visible.

## What is here

- [Vision and falsifiable hypothesis](docs/VISION.md)
- [Evidence-backed competitive assessment](docs/COMPETITORS.md)
- [Requirements](docs/REQUIREMENTS.md), [proposed MVP](docs/MVP.md), and [roadmap](docs/ROADMAP.md)
- [Proposed architecture](docs/ARCHITECTURE.md) and [data model](docs/DATA-MODEL.md)
- [Evaluation strategy](docs/EVALUATION-STRATEGY.md)
- [Open questions and approval gates](docs/OPEN-QUESTIONS.md)
- [Prioritized planning backlog and proposed labels](docs/BACKLOG.md)
- [License decision](docs/LICENSE-DECISION.md)
- [Contribution guidance](CONTRIBUTING.md) and [security reporting](SECURITY.md)

Other planning materials and synthetic examples live under `docs/` and `examples/`. Proposed designs describe intended behavior, not current capabilities.

## What happens next

Review the problem, target user, evidence requirements, scope, and success criteria. Resolve license choice and review the proposed architecture and MVP. Feature implementation must wait for explicit approval of the architecture and MVP. A bounded technical experiment also needs approval of its protocol and execution scope. The planning backlog is not authorization to implement the MVP.

No production traces, customer data, credentials, or private organizational assets belong here. Examples must be synthetic. No external service, model provider, or hosting platform is required to review these documents.

## Status and licensing

The public planning repository is [devSingh29/evaluape](https://github.com/devSingh29/evaluape), on default branch `main`. No CI, infrastructure, deployment, or feature implementation is authorized by that decision.

Open source is the intended direction, but a license has **not** been selected or applied. There is deliberately no `LICENSE` file; this repository does not yet grant an open-source license. See the [conditional recommendation](docs/LICENSE-DECISION.md).

## Start here

Read the [decision brief](docs/DECISION-BRIEF.md) for recommendations, trade-offs and approval questions. See [clean-room design-partner scenarios](docs/DESIGN-PARTNER-SCENARIOS.md) for general-purpose examples and boundaries.

## Before implementation

- [Engineering readiness and scalability](docs/ENGINEERING-READINESS.md)
- [Governance, contribution and future release plan](docs/GOVERNANCE.md)
- [Decision register](docs/DECISIONS.md) and [architecture decision template](docs/ADR-TEMPLATE.md)
- [Ape-themed planning skills](docs/APE-SKILLS.md): Scout, Sleuth, Lab, Guardian, Architect and Review

These are reviewed planning aids, not a claim that runtime controls, CI, releases or diagnostic performance have been implemented. The small local-file exclusion list helps avoid common accidental uploads but is not a secret scanner; review every public change.
