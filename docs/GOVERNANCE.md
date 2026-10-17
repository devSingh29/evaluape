# Governance and release readiness

**Proposed, 17 October 2026.** Evaluape is Planning / Pre-Alpha. No maintainers, review guarantees, branch protections, automation permissions, contribution license, security response team or release process are established by this document. Public planning permission does not approve implementation. Existing [AGENTS.md](../AGENTS.md), [CONTRIBUTING.md](../CONTRIBUTING.md) and [SECURITY.md](../SECURITY.md) remain applicable.

## 1. Roles and decision records

Accountable people must explicitly accept roles. Do not infer a maintainer, copyright holder, security responder or release signer from the repository account name.

| Proposed role | Responsibility | Assignment |
| --- | --- | --- |
| Project decision owner | Approve architecture/MVP, scope, license, budget and release/pilot decisions | Owner identity/decision-record reference to be confirmed; no new delegation implied. |
| Technical reviewer | Review contracts, implementation boundaries, test and migration evidence | To be confirmed. |
| Evaluation reviewer | Freeze rubric/holdout, review leakage and adjudicate evaluation disagreements | To be confirmed; separate from implementation author where feasible. |
| Security contact | Maintain a verified confidential reporting route and coordinate response | To be confirmed before external contribution/release intake. |
| Release/operator owner | Approve artifact provenance, runbooks, recovery and supported versions | To be confirmed before a release or service pilot. |
| Triage owner | Clarify issues, check duplicates and maintain next-action ownership | To be confirmed; no response-time promise. |

One person may hold several roles if disclosed. Do not invent independent review when only one reviewer is available; record the gap and keep the affected gate open. Security-sensitive changes, oracle validation and release approval should obtain a second qualified reviewer before relying on them.

For every consequential decision, record date, approving person, request/reference, exact scope, alternatives, evidence, unresolved risks, reversal cost and next gate. Proposal text, a checklist tick, issue assignment or merged documentation is not execution authorization. Follow [OPEN-QUESTIONS.md](OPEN-QUESTIONS.md) for the approval sequence.

## 2. Contribution and triage proposal

Until licensing and governance are settled, use the existing planning-contribution guidance; do not advertise open code-contribution intake or an implied license grant. Ask the owner to resolve contribution rights before accepting substantial third-party material. No CLA, DCO, code of conduct or license terms are applied by this plan.

Proposed triage flow: new → needs evidence/scope → ready for owner decision → approved planning or separately approved implementation → reviewed → closed with reason. Status labels are concepts, not created repository labels. Each accepted item needs an accountable person, scope, acceptance evidence, authorization gate and next action. Unassigned means unassigned, not silently assigned to the reporter.

- Prefer a minimal synthetic reproduction and expected/observed distinction. Route sensitive reports privately per [SECURITY.md](../SECURITY.md).
- Merge duplicates only after comparing evidence; retain dissent and links. An unresolved claim is not a disproven complaint.
- Explain deferrals and declines briefly. Close with the actual outcome: documented, rejected, superseded, verified or awaiting evidence, rather than implying “fixed.”
- No response SLA is promised. Propose a weekly triage review only after a named maintainer accepts the time commitment.
- Contributor disagreements first receive a written account of evidence and alternatives; unresolved product/scope decisions go to the confirmed decision owner. Safety and authorization gates cannot be bypassed by a popularity vote.

## 3. Branch and draft-PR review policy: proposed, not applied

Approved future implementation uses the `codex/<task-name>` convention already specified in [AGENTS.md](../AGENTS.md). Do not change `main`, configure protection rules, grant permissions or create PRs merely because this policy exists.

Propose small draft PRs while design is uncertain. Their description should identify scope approval, linked decision/issue, affected contracts, synthetic-data assurance, tests actually run versus planned, security/data effects, migration/rollback needs and unresolved questions. Draft status never permits secrets or real traces in the diff.

Before marking ready: self-review the complete diff, verify no generated credentials/private material, update relevant docs, and provide reproducible checks and known limitations. Before merge: obtain review by the confirmed owner/reviewer, resolve blocking feedback, and recheck after material changes. A merge is not release or deployment approval.

After separate settings approval, consider protected `main`, no force pushes, required scoped checks and review, stale-review dismissal on meaningful changes, and explicit review of workflow/release/security files. Do not create fictitious CODEOWNERS entries or require impossible approvals from nonexistent maintainers. Document any emergency exception with reason, actor, scope and retrospective review; exceptions cannot waive external authorization.

## 4. CI and supply-chain plan: no workflow added

Start with a small deterministic, offline suite only after CI approval. Separate untrusted PR validation from trusted release jobs. Proposed controls:

- Minimal read-only job token permissions; explicitly grant only required permissions to individual jobs. No credentials, model-provider calls, production access or package publication in fork PR jobs.
- Avoid privileged `pull_request_target`/`workflow_run` execution of untrusted PR code. Never combine fork code, dependency hooks or PR-controlled scripts with secrets/write tokens. Treat PR titles, artifact contents and metadata as untrusted inputs too.
- Use isolated disposable runners for untrusted work; do not use a runner with a route into a maintainer machine or production network. Separate caches/artifacts across trust boundaries; revalidate anything consumed by privileged jobs.
- Pin reviewed third-party actions to full commit SHAs; review transitive execution and update pins deliberately. Constrain runtime, output size and parallelism to prevent runaway bills. No paid evaluation on arbitrary PRs.
- Lock approved dependencies with integrity metadata where the selected ecosystem supports it. Inventory direct/transitive dependencies, licenses, native binaries and build hooks. Keep optional provider adapters optional.
- Propose vulnerability/license review and a machine-readable SBOM for each release artifact; select a format and generator only after stack review. Triage findings with reachability and severity, a named owner and recorded exceptions, not a badge-only claim.
- Produce checksums and provenance tying each artifact to source commit, builder, inputs and build procedure. Verify from a clean consumer context before release. Provenance does not itself prove code is safe; reproducible-build and SLSA-level claims require separate evidence.
- Publishing credentials, workload identity, environment approvals and repository security features require separate authorization. Prefer a tightly scoped trusted release path after approval; no credential or permission is created here.

These proposals follow GitHub's warnings about untrusted privileged execution and immutable action pinning: [secure use reference](https://docs.github.com/en/actions/reference/security/secure-use) and [pull_request_target guidance](https://docs.github.com/en/actions/reference/security/securely-using-pull_request_target). Provenance vocabulary is informed by [SLSA provenance](https://slsa.dev/spec/v1.2/provenance). Sources checked 17 October 2026; reverify at implementation because platform behavior can change.

## 5. Versioning, release and deprecation proposal

No release is scheduled. A future package could adopt [Semantic Versioning 2.0.0](https://semver.org/), which requires a declared public API and distinguishes initial `0.y.z` development from `1.0.0`. Proposed project convention: document breaking changes even during `0.x`, use minor increments for them, and reserve patches for compatible corrections. This is a convention to approve, not a released compatibility promise.

Schema and adapter versions remain independent; see [ENGINEERING-READINESS.md](ENGINEERING-READINESS.md). Never retag or overwrite an already published release artifact. A correction gets a new version and a clear advisory if relevant.

Before a first release, require:

1. Approved scope and actual architecture/MVP decision; demonstrated acceptance and limitations.
2. Approved license/copyright/contribution terms and third-party attribution review; see [LICENSE-DECISION.md](LICENSE-DECISION.md). No LICENSE is applied here.
3. Named release approver, verified private security route and explicit supported-version policy.
4. Reviewed installation/uninstall path, supported OS/runtime matrix, offline tutorial, dependency inventory, SBOM/provenance and checksums.
5. Schema compatibility tests, migration/restore rehearsal, security review and a statement of what has not been evaluated.
6. Changelog, known issues, rollback/recovery guidance, artifact verification and owner approval for publishing to each destination.

Proposed stable-contract deprecation policy: announce replacement, impacted versions, migration instructions and removal version; allow at least two minor releases and 90 days before removal, unless a separately reviewed urgent safety issue requires faster action. Confirm maintenance capacity before promising that window. During pre-alpha, announce changes prominently without implying supported production use. Security fixes and support end dates need a named owner, not an unlimited maintenance promise.

## 6. Adoption and discoverability: contribution first

Success is repeat useful investigations, credible evidence, easier contribution and lower review burden. Stars and downloads are context, not product validation. No star-chasing, bought engagement, unsolicited promotion, fabricated testimonials or unsupported “first/best” claims.

Checklist before asking others to invest time:

- [ ] Resolve license and contributor rights before calling the repository released open-source software.
- [ ] Keep the planning status and exact approval boundary prominent; distinguish screenshots/storyboards from running product demos.
- [ ] Provide a short offline synthetic walkthrough with input, expected artifact, uncertainty example and explicit limitations. A recorded executable demo waits for build/execution approval.
- [ ] Make the first useful result achievable without accounts, credentials, production access or mandatory provider spend; test this with a fresh user after implementation.
- [ ] Explain fair alternatives and when Evaluape adds no value; link the sourced [competitor review](COMPETITORS.md).
- [ ] Offer bounded beginner-friendly planning tasks with context and acceptance criteria, plus advanced contract/security/evaluation tasks. Confirm reviewers before promising contributor support.
- [ ] Make docs navigable and searchable: glossary, canonical architecture, format examples, troubleshooting and explicit support matrix. Add repository topics/description only under approved settings scope.
- [ ] Publish reproducible positive and negative findings after review; do not reuse public examples as a hidden benchmark.
- [ ] Ask design partners for consented feedback on time to first useful issue, setup burden, repeat use and contribution friction. No trackers, unsolicited outreach or real-data intake is authorized here.

## 7. Risk register and outstanding prerequisites

Every owner below is **to be confirmed**. Proposed roles describe accountability needed, not people already appointed. Review at each gate; a high-risk unresolved item blocks its dependent step.

| Risk | Early signal / proposed mitigation | Owner to be confirmed | Approval prerequisite |
| --- | --- | --- | --- |
| Build starts from a planning checklist | Documentation or issues treated as authorization; require explicit recorded architecture/MVP and bounded scope decision | Project decision owner | Before any implementation, dependency, CI or experimental execution. |
| Platform overbuild without benefit | No measured advantage, shared-user demand or bottleneck; retain offline core and use promotion gates | Technical + product decision owner | Architecture change and operating budget before B/C. |
| Incorrect blame / oracle leakage | Confident unsupported cause, fixture labels in inputs; fresh holdout and independent review | Evaluation reviewer | Approved protocol, isolated oracle and reviewer before scored execution. |
| Private data or prompt injection | Real traces, embedded commands or unsafe exports; synthetic-only planning and explicit boundary validation | Security reviewer | Data-specific approval, threat model and private reporting route before real data. |
| Duplicate publication / overspend | Retry after uncertain send or racing reservations; reconciliation and atomic budgets | Technical reviewer | Destination/action approval and proven recovery before external writes or paid calls. |
| Schema/data loss | Silent conversion, lost unknowns or broken lineage; explicit migrations, backup and restore rehearsal | Data/technical reviewer | Approved contracts and verified reversal plan before destructive migration. |
| Secret exposure through CI | Fork code reaches privileged jobs or caches; segregate trust and minimal permissions | CI/security reviewer | Separate workflow/settings/credential authorization before setup. |
| Supply-chain compromise | Unreviewed hooks, mutable actions or unidentified artifact inputs; pins, inventory and provenance | Release/security reviewer | Dependency and publishing scope approval before installation/release. |
| Unclear license or contribution ownership | Contributors assume rights not granted; resolve holder, license and intake terms | Project decision owner | Before license application, code-contribution acceptance or release. |
| Unowned maintenance / recovery | No responder or failed restore drill; name operators, constrain promises, document support limits | Release/operator owner | Before service pilot, support promises or release. |
| Misleading adoption signals | Stars treated as efficacy, demo presented as product; prioritize documented user value and negative evidence | Product/communications reviewer | Owner review before publication of claims or outreach. |

Readiness summary: planning documents exist; operating policies are proposed; named accountable roles, license and implementation decisions remain open. No settings, enforcement controls or runtime guarantees have been applied.
