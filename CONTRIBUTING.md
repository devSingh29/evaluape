# Contributing during planning

Evaluape currently accepts planning proposals for owner review. No implementation has been approved. A public planning repository under `devSingh29/evaluape` is authorized. Contribution governance and licensing are unresolved; do not assume the scaffold accepts public contributions under an open-source license.

Read [AGENTS.md](AGENTS.md), [the vision](docs/VISION.md), and [open questions](docs/OPEN-QUESTIONS.md) first. Keep proposals bounded and explain what evidence would change your recommendation.

## Useful planning contributions

- Reproducible, entirely synthetic diagnostic cases
- Failure taxonomy and data-contract reviews
- Source-cited competitor comparisons and counterexamples to differentiation
- Evaluation design, baseline selection, and uncertainty-handling proposals
- Privacy and security threat-model reviews without live exploit material

Use the issue templates for planning proposals or synthetic cases. Template labels are proposals until maintainers explicitly create them.

## Diagnostic-case checklist

- [ ] Give the case a stable identifier, version, and concise failure description.
- [ ] State the expected behavior and the observable deviation.
- [ ] Confirm every prompt, trace, tool result, identifier, and output is synthetic.
- [ ] Include sufficient evidence with stable IDs, provenance, and ordering to review the case.
- [ ] Describe missing observations and confounders explicitly.
- [ ] Record at least one plausible competing explanation, or explain why none applies.
- [ ] Keep the diagnostic input separate from evaluation-only oracle labels and hidden fault construction.
- [ ] Specify a proposed intervention and what observation would distinguish the hypotheses.
- [ ] Explain the expected outcome, uncertainty, and when abstention is appropriate.
- [ ] Identify controls, reproducibility assumptions, and possible evaluation leakage.
- [ ] Cite external factual claims with primary-source links and access dates.
- [ ] State approvals and dependencies; do not execute an experiment through an issue submission.

## Evidence is not the oracle

Diagnostic evidence contains only what a diagnosing system or engineer would be allowed to observe. An evaluation oracle contains the fixture author's hidden fault, acceptable answer set, and scoring criteria. Authoring both is useful; giving both to the diagnostic process invalidates the test. A model-generated explanation is a hypothesis, not ground truth.

## Review expectations

Use relative links for repository documents. Label proposed behavior as proposed, distinguish measured findings from estimates, and include limitations. Do not copy private source material or use live data, even if redacted. Do not install dependencies, configure CI, or begin the MVP to demonstrate a planning idea. Ask for a separately scoped experiment approval instead.

For security issues, use [SECURITY.md](SECURITY.md). Never place vulnerabilities, credentials, or private traces in a public issue.
