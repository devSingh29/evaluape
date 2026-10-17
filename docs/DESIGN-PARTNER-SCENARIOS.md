# Design-partner scenarios and clean-room boundary

Status: planning proposal. This public document contains only general-purpose patterns and invented scenarios. It contains no partner code, prompts, schemas, customer records, credentials, or internal business logic.

## Architectural lessons

A document-review workflow motivates independently useful requirements:

- Keep original evidence separate from generated proposals and reviewer corrections.
- Link observations to stable source locations and preserve versions through review.
- Represent missing, extra, duplicated, conflicting and unidentified observations explicitly.
- Distinguish extraction quality from reconciliation, application transformation and preview availability.
- Record the expectation and evidence supporting a correction; a correction is a claim to investigate, not automatically ground truth.
- Bind approval to the exact reviewed revision; retain earlier artifacts without silently rewriting history.
- Make interruption recovery and repeat requests safe, and detect stale concurrent edits.
- Missing values are not automatically zero, false, or a negative finding.

These patterns are architectural references, not a specification to reproduce another product. They should also fit customer support, document processing, coding assistants and internal knowledge tools.

## Synthetic scenarios

| Scenario | Observable contrast | Discriminating test proposed for an approved experiment |
|---|---|---|
| Wrong retrieved context | Output cites a valid passage for the wrong fictional jurisdiction | Hold input/model configuration fixed and replace only the selected context with the matching fixture passage |
| Missing or outdated knowledge | Available fixture corpus lacks the policy effective on the question date | Compare the frozen stale corpus with a versioned updated corpus; distinguish corpus coverage from selection failure |
| Unsupported complaint | User alleges an incorrect total, but source quantities and deterministic arithmetic agree with output | Recompute against an explicit contract; retain uncertainty if the contract itself is disputed |
| Model reasoning mistake | Correct fixture evidence reaches the model, but the final numeric conclusion fails an explicit check | Check arithmetic and compare repeated constrained generations without changing retrieval |
| Schema mapping failure | Raw output is correct but a downstream adapter swaps two field labels | Replay the pure transformation with unchanged raw output and a corrected mapping |
| Application bug blamed on the model | Stored/displayed output differs from the recorded model result | Compare boundaries and replay the affected formatter or state transition using stubs |

All documents, policies, people, organizations, and records in these examples must be invented. Fictional regulatory examples must never be presented as real legal guidance.

## Future integration boundary

A document-extraction application could export a deliberately selected, redacted incident bundle through the neutral contract. A future retrieval-assisted application could contribute source versions, retrieval candidates, selected context and effective-date expectations. Neither integration is configured or authorized by this plan. Live customer data is excluded.

For regulation-oriented retrieval, future requirements include source authority, jurisdiction, effective date, amendment history, coverage gaps and reproducible citations. These are proposed requirements, not claims that any design partner has implemented them. The general-purpose project must not depend on a partner's proprietary architecture or promises of comprehensive legal coverage.

## Approval and publication

The current deliverable is documentation and synthetic planning fixtures only. Architecture and MVP approval are required before implementation. A separate explicit authorization is required before connecting any real system, receiving production data or enabling external writes.
