# Engineering readiness: scale by evidence

**Planning proposal, 17 October 2026.** This is a review checklist, not an implemented platform, benchmark, approved budget, or permission to build. Architecture and MVP approval remain required. No dependencies, executable workflows, service accounts, integrations, or repository settings are created by this document.

Canonical product decisions remain in [ARCHITECTURE.md](ARCHITECTURE.md), [MVP.md](MVP.md), [DATA-MODEL.md](DATA-MODEL.md), and [EVALUATION-STRATEGY.md](EVALUATION-STRATEGY.md). [GOVERNANCE.md](GOVERNANCE.md) covers decision ownership and releases. Avoid copying these contracts into competing specifications.

## 1. Workload envelope and promotion gates

All numbers here are **initial hypotheses to approve and measure**, not supported limits. Benchmark only after execution approval, on a recorded machine/runtime and a frozen synthetic workload. Record warm/cold results, peak memory, payload distributions, throughput, p50/p95 latency, failures, and cost. A threshold triggers a design review, never automatic provisioning.

| Stage | Proposed measurement envelope | Evidence needed before changing architecture |
| --- | --- | --- |
| A: offline, file-first V0 | One operator, one active investigation; 100 investigations/day for a stress scenario, 10 MiB typical and 100 MiB maximum uncompressed bundle; at most 10,000 artifacts per bundle; 10 GiB retained local corpus | Start here. Validate utility and safe bounded import before optimizing throughput. Large archives and nested content count against decompressed limits; do not silently truncate evidence. |
| A → B: modular shared service | Propose a trial envelope of five concurrent investigators and 1,000 investigations/day; burst arrival rate and work duration must be specified separately | At least two independently operated pilot teams need shared review/access controls, or approved target workload misses p95 budgets in three reproducible runs after local profiling. Require explicit service, privacy, operational-owner and spend approvals. Shared identity needs can justify B without high volume. |
| B → C: distributed workflows/services | No committed capacity target; obtain measured arrival/service-time distributions, peak concurrency, data growth and failure/recovery needs first | In an approved representative load test, queue wait p95 exceeds 60 seconds or a critical resource stays above 70% utilization for 30 minutes after bounded tuning/worker scaling, across three runs; alternatively, at least two accountable teams demonstrably need independent release or isolation boundaries. An ADR must show why B cannot meet the agreed target more simply. |

Do not infer a service tier from daily counts alone: 1,000 evenly spaced jobs and 1,000 simultaneous jobs are different workloads. Capacity planning should use measured arrival rate × mean service time for average concurrency, then test bursts, tail durations, cancellations and failures explicitly. Reserve headroom and test the smallest useful deployment first. Stars, a hypothetical enterprise customer, or a large architecture diagram are not migration triggers.

## 2. Performance, cost and capacity hypotheses

| Area | Initial proposal | Acceptance evidence / action on breach |
| --- | --- | --- |
| Offline deterministic path | On an agreed 4-core/8 GiB reference machine: p95 import + deterministic checks + local export ≤5 seconds for a 10 MiB fixture; peak process RSS ≤512 MiB | Separate filesystem cold/warm runs; exclude optional model/replay time and report those separately. A breach prompts profiling or a smaller documented envelope, not a correctness shortcut. |
| Bounded import | 100 MiB decompressed bytes and 10,000 artifacts per bundle; reject absolute paths, traversal, links escaping the import root and malformed references | Test boundary-minus-one/boundary/over-limit cases, archive expansion and deeply nested inputs. Return an explicit rejected/partial state; never claim completeness after loss. |
| Experiment execution | Use the canonical per-case token/tool/intervention/time caps in [EVALUATION-STRATEGY.md](EVALUATION-STRATEGY.md) | Apply the canonical per-case cap separately to each experimental arm, counting that arm's retries, failed attempts and all model paths. Separately account for the approved study-wide total across every case, arm and repeat. Define whether restoration runs consume intervention allowance before protocol approval. No new or larger allowance is granted here. |
| Money | Offline deterministic operation has no required paid provider; hosted/model USD ceilings remain unapproved | Budget = measured per-case provider/tool cost × all planned cases/arms/repeats + approved reserve, plus storage/egress/compute. Reserve atomically; stop at the approved total. Never equate token limits with dollar limits. |
| Storage | 100 × 10 MiB/day is about 1 GiB/day before derivatives, indexes and backup copies | Measure amplification; calculate retention from approved policy rather than silently deleting. Warn at 70% of an approved disk quota and refuse new work before reserved headroom is exhausted. Test low-disk recovery. |
| Future service reliability | Illustrative pilot goal: 99.5% successful eligible control-plane requests over a rolling 30-day window; queue p95 ≤60 seconds under the approved envelope | Define the request denominator, exclusions and separate dependency/replay failures before use. No uptime promise exists. Establish an operator and response plan before a service pilot. |

Keep workload versions and performance results alongside the decision record. Comparison runs must use the same evidence and hardware envelope; compare quality and cost together. None of these performance hypotheses overrides the diagnostic safety gates.

## 3. Contract seams and compatibility

The deterministic core should accept explicit immutable inputs and return structured results. Inject clock, randomness and filesystem/provider effects through boundaries. Core verdicts must not depend on network availability, provider branding, or an implicit global workspace. Optional model output is an untrusted suggestion. Replay execution, persistence, import, model access and publication belong behind the adapter contracts in [ARCHITECTURE.md](ARCHITECTURE.md).

Before implementation, enumerate the public surface: bundle schema, stable identifiers and locators, CLI flags/exit codes, structured output, adapter capabilities, and error taxonomy. Human-readable prose is not a machine API unless explicitly designated. Define canonical serialization/hashing rules before relying on digest equality, including encoding, number handling and field order. Preserve original evidence bytes; canonical representations are separate derived artifacts.

Proposed evolution policy:

- Version bundle/schema contracts independently from package versions and record both. Every adapter declares supported versions and capabilities; unsupported required semantics fail explicitly.
- Optional additive fields may be compatible only if old readers retain meaning. New required fields, changed verdict meaning, removed enum values or changed approval semantics require a breaking contract version.
- Unknown data fields can remain in a bounded extension envelope; unknown control/capability/approval fields fail closed. Unknown enum values must not silently become `unsupported`, `approved` or a default tenant.
- Maintain fixtures for each supported read version and a declared writer version. Initial support-window proposal: current and previous schema major, only if maintenance capacity is approved; no indefinite compatibility promise.
- Migration emits source/destination versions, tool version, input/output digests, loss/unknown-field report and lineage. Never silently rewrite historical evidence or transfer approval authority between installations.
- Use expand → migrate → verify → contract for a future shared store. Do not remove old read paths until a restore/reversal test and consumer inventory pass. Offline upgrades create a new bundle and preserve the original until verified.

## 4. Reliability and concurrency invariants

The invariants in [DATA-MODEL.md](DATA-MODEL.md) remain authoritative. The future implementation review must demonstrate:

1. Atomic local manifest publication: stage and verify artifacts before publishing a complete manifest; recover interrupted writes without declaring absent bytes complete.
2. Revision-checked state transitions; a stale worker or approval cannot modify a newer investigation. Leases require fencing generations, not expiry checks alone.
3. Separate idempotency identities for ingestion, analysis jobs and external publication. At-least-once work does not imply exactly-once external effects.
4. Future durable job creation coordinated with state changes; a transactional outbox is a candidate for B, not a required V0 service.
5. Bounded retries with error classification, backoff and cancellation. Provider timeouts after a write produce `uncertain`; reconcile with the destination before any repeat. If reconciliation cannot establish the result, stop for review.
6. Atomic reservations for cost and resources; release unused reservations on terminal states without forgetting actual consumption. Crash recovery cannot create a second spend allowance.
7. Tenant scope and capabilities checked at every boundary; no shared-service claim based on offline workspace labels. Replay descendants must stop on cancellation and capability expiry.
8. Backpressure and explicit queue/resource limits; overload rejects or defers work visibly instead of dropping evidence or making an unsupported diagnosis.

## 5. Test layers to authorize later

| Layer | Proposed coverage | Gate |
| --- | --- | --- |
| Static/doc checks | Local links, schema examples, terminology, formatting, dependency/license inventory once dependencies exist | Planning artifacts can be manually reviewed now; automated checks are proposed, not installed. |
| Deterministic unit + property tests | Verdict guards, missingness, digest handling, budgets, tenant references, state transitions; same inputs produce same structured result | Required before a technical spike is called correct. |
| Contract + golden fixtures | Supported schema versions, all adapter error modes, import/export lineage and round trips | Independent fake adapters; no live account requirement. |
| Adversarial input/security | Path/archive bombs, malformed sizes, forged approvals, injection in evidence, cross-workspace references, oracle access | Synthetic bounded payloads in an isolated approved harness; no testing third-party systems. |
| Recovery/concurrency | Crash at each durable boundary, duplicate delivery, expired leases, reordered jobs, cancellation, disk full, reconciliation ambiguity | Assert no duplicated consequential effect or budget overrun; preserve unresolved states. |
| Integration/end-to-end | Offline complaint → evidence → reviewed diagnosis → local issue/regression export; negative and incomplete cases | First prove without a provider/network. Any provider/test-service path needs separate scope approval. |
| Performance + reliability | Envelope, burst/soak, memory/storage growth and recovery; future service isolation | Record measurements and failures, not just a green pass. |
| Diagnostic validity | Fresh locked holdout, fair baselines, blinded review, actual approved interventions | [EVALUATION-STRATEGY.md](EVALUATION-STRATEGY.md) governs. Public illustrations and passing code tests cannot establish efficacy. |

## 6. Backup, restore and migration rehearsal

For V0, propose an explicit export of manifests plus referenced retained artifacts, checksums, schema/runtime metadata and review history. Credentials are excluded. Verify completeness and restore into a separate workspace; restored approvals are history, not permission to publish. Repository history is not a backup of runtime evidence.

Before a shared service, name an operational owner and approve storage location, access, encryption/key recovery, retention, deletion propagation and costs. Initial pilot recovery hypotheses are **RPO ≤24 hours and RTO ≤4 hours**, subject to actual user needs. No backup system or recovery guarantee exists. Coordinate database snapshots and blob inventory; verify every required reference, and document unavailable/deleted evidence explicitly.

Rehearse restore before each storage/schema-breaking release and propose a monthly pilot drill thereafter. Record elapsed recovery time, recovered revision, integrity checks and unresolved gaps. Retention/deletion requirements apply to derivatives and expiring backups; external exports require separate remediation. Backups must not resurrect revoked access or quietly recreate deliberately deleted evidence.

## 7. Readiness snapshot

“Complete” below means the named planning artifact exists, not that its proposal is approved or implemented.

| State | Item | Remaining evidence |
| --- | --- | --- |
| Complete: documented | Offline-first architecture alternatives, conceptual data model, narrow MVP and evaluation protocol | Owner decisions and execution evidence still absent. |
| Complete: documented | Engineering review checklist, migration triggers and governance proposal | Review and assignment required. |
| Proposed | Workload caps, latency/capacity hypotheses, compatibility window, recovery targets | Approved workload and reproducible measurements. |
| Proposed | Test layers, CI/release isolation and supply-chain controls | Separately approved implementation and verified results. |
| Blocked on approval | Architecture + MVP + stack + bounded experiment | Record actual approving owner, date, scope, budget and reference. |
| Blocked on decisions | License/copyright, security contact, accountable reviewers/operators | See [OPEN-QUESTIONS.md](OPEN-QUESTIONS.md) and [GOVERNANCE.md](GOVERNANCE.md). |
| Not implemented | Application, adapters, CI, build, deployment, backup and release tooling | This plan authorizes none of them. |
