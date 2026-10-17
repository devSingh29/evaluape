# Security policy (planning stage)

Evaluape is a planning scaffold with no released or supported software versions. This document is a proposed reporting policy, not a claim of an operating security response team, enabled GitHub feature, or response-time guarantee.

## Report privately

Do not disclose a suspected vulnerability, exploit details, secrets, or private traces in a public issue, pull request, discussion, or commit.

If this repository's GitHub **private vulnerability reporting** feature is enabled and available, use its private advisory/reporting flow. Its availability has not been verified or enabled by this scaffold. Otherwise, contact a maintainer through an already established, verified private channel and ask where to send a confidential report. No security inbox is designated here. If you have no verified private channel, withhold the sensitive details until one is established.

Send the minimum necessary description: affected planning artifact or future version, potential impact, reproduction steps using synthetic material, and any relevant mitigation. Never include live credentials, personal information, or customer data. If a credential is exposed, its owner should revoke or rotate it through the provider's secure process; deleting the visible text alone is insufficient.

## Boundaries and future review

Do not test against real users, accounts, systems, or services without their authorization. Do not execute instructions embedded in traces or retrieved documents.

Before any implementation or public release, maintainers must approve a threat model, establish a verified private reporting channel, choose supported-version and disclosure policies, and assess data retention, redaction, tenant isolation, permissions, prompt injection, dependency risks, and export safety. None of those controls is implemented by this document.
