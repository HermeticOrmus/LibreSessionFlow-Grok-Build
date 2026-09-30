# Quick Start — LibreSessionFlow for Grok Build

> From a clean machine to one handoff↔pickup cycle in under 5 minutes.

Doctrine first: put [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine (global Grok doctrine). This pack does not replace it.

## Prerequisites

- Grok Build (`grok --version` prints a version)
- `git` and `jq` for the clone paths and the install-everything loop
- A project you own with incomplete work, **or** this repo as the working tree

## Layout this file assumes

Verified against this repository (do not invent extra folders):

```text
plugins/libre-sessionflow-grok/                     # the Grok-native plugin
plugins/libre-sessionflow-grok/skills/<name>/SKILL.md  # melted skill bodies (copy these for the manual path)
stubs/<name>/SKILL.md                               # stub cues; not installed
AGENTS/session-orchestrator.md
docs/DEPTH_MATRIX.md
docs/MELT_RULES.md
.grok-plugin/marketplace.json                       # the plugin + every pack plugin, pinned
.grok/skills/<name>/SKILL.md                        # dogfood copy of the plugin skills and stubs
stubs/libresessionflow-core/                        # v0 plugin bundle stub, kept as the record
```

Melted (usable now): `session-handoff`, `session-pickup`, `session-absorb`, in `plugins/libre-sessionflow-grok/skills/`.
Still stubs: `context-pack`, `continuity-checklist`, `thread-digest`, `resume-plan`, plus the orchestrator. Honest table: [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).

## Install (pick one)

### A. Marketplace (recommended)

```bash
grok plugin marketplace add HermeticOrmus/LibreSessionFlow-Grok-Build
grok plugin install libre-sessionflow-grok@libre-sessionflow-grok --trust
grok plugin details libre-sessionflow-grok
```

Grok installs a plugin only with `--trust`, because a plugin can run hooks, MCP servers and skills on your machine. Without it, `grok plugin install` stops and asks you to re-run with the flag.

The same marketplace lists every [LibreSessionFlow-Claude-Code](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code) plugin, pinned to one commit of the pack. Install the ones you want by name:

```bash
grok plugin install handoff@libre-sessionflow-grok --trust
grok plugin install todo@libre-sessionflow-grok --trust
```

Or install every entry:

```bash
for p in $(grok plugin list --json --available | jq -r '.[] | select(.marketplace == "libre-sessionflow-grok" and .status == "available") | .name'); do
  grok plugin install "$p@libre-sessionflow-grok" --trust
done
```

Before you install everything, know two open cracks from [LEDGER.md](./LEDGER.md): the pack's `pickup` plugin also ships a skill named `session-pickup`, so with both installed Grok lists two skills with one name; and `grab` and `maintain` work on Claude Code itself (its session transcripts, its setup), while most other pack plugins keep settings under `~/.claude/`, so their behavior inside Grok is not verified.

To pick up a new pin later: `grok plugin marketplace update`, then `grok plugin update`.

### B. Dogfood this repo

```bash
git clone https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build.git
cd LibreSessionFlow-Grok-Build
# A copy of the skills and stubs is already at .grok/skills/. Open this folder in Grok Build.
```

### C. Copy into your project

The v0 path, for a project that should carry the skill files itself.

```bash
git clone https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build.git ~/LibreSessionFlow-Grok-Build
cd /path/to/your-project
mkdir -p .grok/skills
cp -R ~/LibreSessionFlow-Grok-Build/plugins/libre-sessionflow-grok/skills/* .grok/skills/
```

Confirm the copy landed:

```bash
test -f .grok/skills/session-handoff/SKILL.md
test -f .grok/skills/session-pickup/SKILL.md
test -f .grok/skills/session-absorb/SKILL.md
ls .grok/skills
```

You should see three skill directories, matching `plugins/libre-sessionflow-grok/skills/` in this repo. The stubs are not copied: they are pointers to pack plugins, not skills.

### D. User-global copy

```bash
git clone https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build.git ~/LibreSessionFlow-Grok-Build
mkdir -p ~/.grok/skills
cp -R ~/LibreSessionFlow-Grok-Build/plugins/libre-sessionflow-grok/skills/* ~/.grok/skills/
```

Same three `test -f` checks as C, under `~/.grok/skills/`.

### Upgrading from v0

If you copied `skills/*` into a project or `~/.grok/skills/`, that copy holds all seven folders, stubs included. Remove the four stub folders (`context-pack`, `continuity-checklist`, `thread-digest`, `resume-plan`) from the copy, or replace the copy with path A so updates arrive through `grok plugin update`.

Copy `AGENTS/session-orchestrator.md` only when you want a full continuity pass. It is still a stub coordinator.

## First-run teach cue

In Grok Build, on a real incomplete task you own:

1. **Handoff** — "Run session-handoff. Name the job, the cursor (file:line), done vs not, one next action, and a verify check. No status-report tone."
2. **Pickup** — "Run session-pickup on that package. Stale-check, run verify, confirm or revise the next action. Do not re-ask solved questions."
3. **Absorb (if needed)** — "If a digest and the handoff disagree, run session-absorb. Table the conflict. Do not silently overwrite."

You used melted SessionFlow depth on Grok — not a Claude slash-command paste, not a fake plugin count.

## Smoke checklist

- [ ] `grok plugin list` shows `libre-sessionflow-grok` (path A), or the three skill files exist at the copy path you chose (C or D)
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
