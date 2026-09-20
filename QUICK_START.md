# Quick Start — LibreSessionFlow for Grok Build

> From a clean machine to one handoff↔pickup cycle in under 5 minutes.

Doctrine first: put [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine (global Grok doctrine). This pack does not replace it.

## Prerequisites

- `git`
- Grok Build installed and able to see skills under `.grok/skills/` or `~/.grok/skills/`
- A project you own with incomplete work, **or** this repo as the working tree

## Layout this file assumes

Verified against this repository (do not invent extra folders):

```
skills/<name>/SKILL.md                 # canonical skill bodies (copy these)
AGENTS/session-orchestrator.md
docs/DEPTH_MATRIX.md
docs/MELT_RULES.md
.grok/skills/<name>/SKILL.md           # dogfood copy; must match skills/
.grok/plugins/libresessionflow-core/   # plugin stub; not required for first run
```

Melted (usable now): `skills/session-handoff/SKILL.md`, `skills/session-pickup/SKILL.md`, `skills/session-absorb/SKILL.md`.
Still stubs: `context-pack`, `continuity-checklist`, `thread-digest`, `resume-plan`, plus the orchestrator. Honest table: [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).

## Install (pick one)

### A. Dogfood this repo (fastest)

```bash
git clone https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build.git
cd LibreSessionFlow-Grok-Build
# Skills are already at .grok/skills/ — open this folder in Grok Build.
```

### B. Install into your project

```bash
git clone https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build.git ~/LibreSessionFlow-Grok-Build
cd /path/to/your-project
mkdir -p .grok/skills
cp -R ~/LibreSessionFlow-Grok-Build/skills/* .grok/skills/
```

Confirm the copy landed:

```bash
test -f .grok/skills/session-handoff/SKILL.md
test -f .grok/skills/session-pickup/SKILL.md
test -f .grok/skills/session-absorb/SKILL.md
ls .grok/skills
```

You should see seven skill directories, matching `skills/` in this repo.

### C. User-global

```bash
git clone https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build.git ~/LibreSessionFlow-Grok-Build
mkdir -p ~/.grok/skills
cp -R ~/LibreSessionFlow-Grok-Build/skills/* ~/.grok/skills/
```

Same three `test -f` checks as B, under `~/.grok/skills/`.

Copy `AGENTS/session-orchestrator.md` only when you want a full continuity pass. It is still a stub coordinator.

## First-run teach cue

In Grok Build, on a real incomplete task you own:

1. **Handoff** — "Run session-handoff. Name the job, the cursor (file:line), done vs not, one next action, and a verify check. No status-report tone."
2. **Pickup** — "Run session-pickup on that package. Stale-check, run verify, confirm or revise the next action. Do not re-ask solved questions."
3. **Absorb (if needed)** — "If a digest and the handoff disagree, run session-absorb. Table the conflict. Do not silently overwrite."

You used melted SessionFlow depth on Grok — not a Claude slash-command paste, not a fake plugin count.

## Smoke checklist

- [ ] `session-handoff`, `session-pickup`, and `session-absorb` files exist at the install path you chose
- [ ] Grok can see those three skills
- [ ] One handoff produced with job, cursor, verify, and a concrete next action (not "continue")
- [ ] One pickup resumed without re-asking a solved question
- [ ] No secrets in the package, examples, or prompts

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- This pack: [LibreSessionFlow-Grok-Build](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build)
- Sibling Libre*-Grok-Build packs: [Arch](https://github.com/HermeticOrmus/LibreArch-Grok-Build) · [Copy](https://github.com/HermeticOrmus/LibreCopy-Grok-Build) · [DevOps](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build) · [Embed](https://github.com/HermeticOrmus/LibreEmbed-Grok-Build) · [FinTech](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build) · [GameDev](https://github.com/HermeticOrmus/LibreGameDev-Grok-Build) · [GEO](https://github.com/HermeticOrmus/LibreGEO-Grok-Build) · [MLOps](https://github.com/HermeticOrmus/LibreMLOps-Grok-Build) · [MobileDev](https://github.com/HermeticOrmus/LibreMobileDev-Grok-Build) · [SecOps](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build) · [UIUX](https://github.com/HermeticOrmus/LibreUIUX-Grok-Build) · [WhatsApp](https://github.com/HermeticOrmus/LibreWhatsApp-Grok-Build)
- Skills collections: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof (upstream, not this inventory): [LibreSessionFlow-Claude-Code](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code)
- https://ormus.solutions
