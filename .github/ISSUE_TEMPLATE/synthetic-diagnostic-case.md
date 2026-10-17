---
name: Synthetic diagnostic case
about: Propose an entirely synthetic case with separate evidence and oracle material
title: ''
---

## Case identity and expected behavior

Stable ID/version, intended behavior, and observable failure.

## Diagnostic evidence

Provide only synthetic evidence visible to a future diagnostic process. Include stable evidence IDs, provenance, ordering, and missing observations. Do not insert the hidden fault or answer here.

## Competing explanations and discriminating test

Describe alternatives and the proposed intervention/control. A proposed test is not permission to execute it.

## Evaluation-only oracle

Link a clearly separated evaluation-only artifact containing the hidden fault and scoring criteria. Do not include it in diagnostic inputs. Explain expected abstention or acceptable alternatives when the case is ambiguous.

## Reproducibility and leakage risks

State assumptions, stochastic effects, case-author clues, and limitations.

## Checklist

- [ ] All material is synthetic, not redacted real data.
- [ ] No secrets, personal information, customer traces, or private URLs are included.
- [ ] Evidence and oracle are separate.
- [ ] Expected behavior and failure are explicit.
- [ ] Missing evidence and competing hypotheses are addressed.
- [ ] External factual claims have primary-source citations and review dates.
- [ ] Acceptance criteria, dependencies, and approvals are identified.

For suspected vulnerabilities or secret exposure, do not use this issue: follow SECURITY.md privately.
