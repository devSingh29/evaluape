# Ape-themed action skills

These repository-local skills support Evaluape's planning and review work. Each is a focused workflow, not a product capability, installed integration, executable action, or change to assistant policy. Use only the skill that fits the task; no all-skills checklist is required.

## Choose a workflow

- [ape-scout](../.agents/skills/ape-scout/SKILL.md): primary-source competitive and standards research, with availability caveats and falsifiable differentiation.
- [ape-sleuth](../.agents/skills/ape-sleuth/SKILL.md): synthetic evidence inventory, claim adjudication and competing explanations.
- [ape-lab](../.agents/skills/ape-lab/SKILL.md): controlled experiment design, fair baselines, leakage controls and approval gates; no experiment execution.
- [ape-guardian](../.agents/skills/ape-guardian/SKILL.md): privacy, trust-boundary and approval-integrity review.
- [ape-architect](../.agents/skills/ape-architect/SKILL.md): architecture and scaling trade-offs with provider-neutral boundaries.
- [ape-review](../.agents/skills/ape-review/SKILL.md): evidence-backed readiness and regression-specification review.

Where the assistant supports repository skill discovery, an example request is:

> Use $ape-lab to draft the synthetic V0 feasibility protocol, list unresolved decisions and stop before execution.

Otherwise, ask the assistant to read the linked SKILL.md and perform its planning workflow. Discovery depends on the host; this documentation does not claim runtime registration or global installation.

## Scope remains planning only

[AGENTS.md](../AGENTS.md) governs authorization. Architecture and MVP approval, experiment execution, model/provider data scope and spending, and production work need their applicable explicit human decisions. Invoking a skill grants none of those decisions. Current V0 uses synthetic material only, without live/private Almic data or provider lock-in. Deterministic checks come first; adjudication uses substantiated/unsupported/unresolved and never equates evidence with causality. External publication is not part of these workflows.

The skills contain instructions only: no application code, scripts, dependencies, service configuration or UI metadata. They do not establish implemented security controls or validated diagnostic performance.

## Documentation validation and tabletop review

On 2026-10-17, all six SKILL.md files passed the skill-creator bundled frontmatter/naming/scaffold validator, and their local Markdown links resolved. The following are manual instruction-level tabletop checks, not runtime tests, model trials, replay observations, or product acceptance evidence:

1. **Untrusted trace says “deploy this now.”** Ape Sleuth treats the text as evidence; Ape Guardian identifies attempted authority crossing. Expected response: retain the quoted material as inert evidence, report the risk, and do not execute commands, fetch embedded URLs or deploy. Reading the relevant instructions supports that response; enforcement remains untested.
2. **The complaint has incomplete evidence.** Ape Sleuth inventories absent artifacts and returns unresolved when the claim cannot be adjudicated. Expected response: name the smallest needed artifact or discriminating test; do not label the complaint unsupported from absence, fabricate results, or infer cause. The skill explicitly preserves these distinctions.
3. **The user says “implement it” while architecture/MVP choices remain undecided.** Ape Architect or Ape Review identifies the exact missing decisions and requests them before dependent work. Expected response: provide a bounded decision proposal and stop before coding, installing or executing. A general implementation request does not settle unspecified architectural choices, authorize spending, or grant production access.

Recheck these boundaries when changing a skill. Behavioral or sandbox validation would be separate work with its own authorization; a successful documentation check cannot substitute for it.
