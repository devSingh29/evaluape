# Vision

**Status: hypothesis for review, not a validated product claim.**

## Problem and intended user

An engineer investigating an AI application failure may have traces and evaluation results yet still need to decide which explanation to test next. Scores identify a problem; diagnosis requires connecting evidence to competing hypotheses, testing a change, and checking whether the apparent improvement generalizes.

The proposed initial user is an engineer responsible for a small, tool-using or retrieval-assisted AI application. That persona and the importance of this problem remain assumptions to validate.

## Hypothesis

A portable, evidence-linked diagnostic workflow can reduce the effort needed to identify a defensible next experiment on a reproducible failure, while avoiding confident explanations unsupported by the available observations.

A proposed workflow is:

1. Describe expected behavior and the observable failure.
2. Assemble bounded evidence with provenance and missing-data markers.
3. Form competing hypotheses and cite supporting and conflicting evidence.
4. Propose a discriminating intervention, control, and expected observations.
5. After separate approval, run the bounded experiment and evaluate outcomes.
6. Retain, revise, or reject the hypothesis; abstain when evidence is insufficient.

The desired output is an auditable diagnostic record, including uncertainty and a useful next test. A persuasive narrative alone does not satisfy the hypothesis.

## Candidate differentiation, still unproven

LangSmith Engine, Raindrop, Braintrust, and Arize AX are serious competitors or adjacent alternatives. Their existence rules out assuming that AI-assisted diagnosis or debugging is a unique idea. Compare current primary-source capabilities before making any feature-gap claim.

Potential value to test is the combination of portable evidence contracts, explicit competing hypotheses, reproducible interventions, and clear separation of diagnostic inputs from evaluation oracles. Each element may already exist elsewhere. Whether the combined workflow is useful, better, or worth adopting is an open empirical question.

## What would weaken or refute the idea?

- Existing tools or a simple baseline yield equally actionable diagnoses with less effort.
- The proposed workflow produces plausible explanations but cannot distinguish causes.
- Gains disappear when oracle leakage and case-author clues are removed.
- Portability removes too much context to support a useful diagnosis.
- Engineers find evidence preparation more expensive than direct debugging.
- Missing data leads to confident wrong claims instead of abstention.

## Boundaries

Evaluape is independent of Almic. Public planning under `devSingh29/evaluape` is authorized. Open-source licensing remains pending an explicit license decision; public visibility alone does not establish an open-source license. It currently implements none of the workflow above.

The immediate outcome is an approved or rejected research plan. A technical experiment, provider integration, live-data study, and production system each require a separate explicit scope decision. Planning does not authorize executing the MVP.
