<p align="center">
  <img src="https://ormus.solutions/mascot/pixellab_liquid_to_ouroboros.gif" alt="LibreSessionFlow Grok Build" width="128" style="image-rendering: pixelated;" />
</p>

<h1 align="center">LibreSessionFlow Grok Build</h1>

<p align="center">
  <em>Session handoff, pickup, and absorb for Grok Build: Grok-native skills plus every LibreSessionFlow pack plugin, from one marketplace</em>
</p>

<p align="center">
  <a href="https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/stargazers"><img src="https://img.shields.io/github/stars/HermeticOrmus/LibreSessionFlow-Grok-Build?style=flat-square&color=aa8142" alt="Stars" /></a>
  <a href="https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/blob/main/LICENSE"><img src="https://img.shields.io/github/license/HermeticOrmus/LibreSessionFlow-Grok-Build?style=flat-square&color=aa8142" alt="License" /></a>
  <a href="https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/commits"><img src="https://img.shields.io/github/last-commit/HermeticOrmus/LibreSessionFlow-Grok-Build?style=flat-square&color=aa8142" alt="Last Commit" /></a>
  <img src="https://img.shields.io/badge/Session_Lifecycle-aa8142?style=flat-square" alt="Session Lifecycle" />
  <img src="https://img.shields.io/badge/Grok_Build-aa8142?style=flat-square&logo=x&logoColor=white" alt="Grok Build" />
</p>

---

**Session handoff, pickup, and absorb for [Grok Build](https://github.com/HermeticOrmus/grok-build-reality-os)** — ported and melted from [LibreSessionFlow-Claude-Code](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code), not a dumb copy.

> Status: **v1.0.0**. Three skills are melted into the Grok-native plugin `libre-sessionflow-grok` (`session-handoff`, `session-pickup`, `session-absorb`). The other four are honest stubs in [stubs/](./stubs/), each naming the pack plugin nearest to the real depth. See [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md) and the [kintsugi ledger](./LEDGER.md).

## Why this exists

Long agent sessions lose context. SessionFlow owns handoff / pickup / absorb patterns so the next turn (or next human) can resume without archaeology. Grok Build needs the same *job* with Grok-native skills, agents, `.grok/`, and truth-seeking voice. This repo counts only what it has melted.

## Install

One marketplace brings both layers: the Grok-native plugin melted here, and every plugin of the [LibreSessionFlow-Claude-Code](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code) pack, pinned to one commit of the pack. Grok reads the pack plugins as they are.

```bash
grok plugin marketplace add HermeticOrmus/LibreSessionFlow-Grok-Build
grok plugin install libre-sessionflow-grok@libre-sessionflow-grok --trust
```

Grok installs a plugin only with `--trust`, because a plugin can run hooks, MCP servers and skills on your machine. Read what you trust: each entry's source is linked in [.grok-plugin/marketplace.json](./.grok-plugin/marketplace.json).

Then add the pack plugins you want, for example:

```bash
grok plugin install handoff@libre-sessionflow-grok --trust
grok plugin install todo@libre-sessionflow-grok --trust
```

Two things to know before you install the whole pack (both in the [ledger](./LEDGER.md)): the pack's `pickup` plugin also ships a skill named `session-pickup`, so installing it next to `libre-sessionflow-grok` gives Grok two skills with one name; `grab` and `maintain` work on Claude Code itself (its session transcripts, its setup), and most other pack plugins keep their settings and handoff index under `~/.claude/`, so their behavior inside Grok is not verified.

[QUICK_START.md](./QUICK_START.md) has the loop that installs every entry, the dogfood clone, and the manual copy path. From a clone:

```bash
git clone https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build.git
cd LibreSessionFlow-Grok-Build
# Dogfood: .grok/skills/ holds a copy of the skill bodies and stubs.
# Other project: cp -R plugins/libre-sessionflow-grok/skills/* /path/to/your-project/.grok/skills/
```

Doctrine: install [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine first. Do not replace doctrine with this pack.

## Depth (honest)

| Artifact | This repo now | Where |
|----------|---------------|-------|
| Grok-native skills | 3 melted | `plugins/libre-sessionflow-grok/skills/` |
| Stub skills | 4, not installed | `stubs/`, each names its nearest pack plugin |
| Agents | 1 stub (`session-orchestrator`), not installed | `AGENTS/` |
| Plugins in the marketplace | 1 Grok-native + 10 pack entries | `.grok-plugin/marketplace.json`, pinned to one pack commit |

Pack entries are LibreSessionFlow-Claude-Code plugins installed through this marketplace. They are not melted here, and they are not counted as this repo's skills. Do not paste Claude plugin/agent/command totals here. Update [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md) when something melts, and run `scripts/pin-pack.sh` when the pack changes.

## Skills

| Skill | Status | Job | Pack plugin |
|-------|--------|-----|-------------|
| session-handoff | melted | Write a pickable handoff package | melted from `handoff` |
| session-pickup | melted | Resume from a handoff without re-discovery | melted from `pickup` |
| session-absorb | melted | Fold scattered sources; surface conflicts | melted from `absorb` |
| context-pack | stub | Compress goals / decisions / loops | nearest: `handoff` |
| continuity-checklist | stub | End-of-session smoke | real depth in `close` |
| thread-digest | stub | Summarize a thread for action | nearest: `close` |
| resume-plan | stub | Next 3 actions after pickup | nearest: `pickup` |

Agent: `AGENTS/session-orchestrator.md` — stub coordinator for a full handoff↔pickup pass.

## Layout (Grok Build)

```text
plugins/libre-sessionflow-grok/  # the Grok-native plugin: manifest + melted SKILL.md bodies
stubs/                           # stub skills + the v0 bundle stub; not installed
AGENTS/                          # suite agents
docs/                            # DEPTH_MATRIX, MELT_RULES
scripts/pin-pack.sh              # re-pins the pack entries to the pack's main
.grok-plugin/                    # marketplace: the plugin + every pack plugin, pinned
.grok/skills/                    # dogfood copy of the plugin skills and stubs (CI checks it)
```

Claude's `.claude/` maps to Grok skills + `AGENTS.md` + `.grok/`. Melt rules: [docs/MELT_RULES.md](./docs/MELT_RULES.md).

## Kintsugi ledger

Every crack found in v0 and how this release seals it, with the file that shows the seal, plus the cracks still open: [LEDGER.md](./LEDGER.md).

## Feedback and contributing

Tell us what worked and what is missing with the [feedback form](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/issues/new?template=feedback.yml). When Grok picks the wrong skill, file a [routing miss](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/issues/new?template=routing-miss.yml). Ways to contribute are in [CONTRIBUTING.md](./CONTRIBUTING.md).

## Gold Hat

[GOLD_HAT.md](./GOLD_HAT.md) — empower or extract?

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- This pack: [LibreSessionFlow-Grok-Build](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build)
- Sibling Libre*-Grok-Build packs: [Arch](https://github.com/HermeticOrmus/LibreArch-Grok-Build) · [Copy](https://github.com/HermeticOrmus/LibreCopy-Grok-Build) · [DevOps](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build) · [Embed](https://github.com/HermeticOrmus/LibreEmbed-Grok-Build) · [FinTech](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build) · [GameDev](https://github.com/HermeticOrmus/LibreGameDev-Grok-Build) · [GEO](https://github.com/HermeticOrmus/LibreGEO-Grok-Build) · [MLOps](https://github.com/HermeticOrmus/LibreMLOps-Grok-Build) · [MobileDev](https://github.com/HermeticOrmus/LibreMobileDev-Grok-Build) · [SecOps](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build) · [UIUX](https://github.com/HermeticOrmus/LibreUIUX-Grok-Build) · [WhatsApp](https://github.com/HermeticOrmus/LibreWhatsApp-Grok-Build)
- Skills collections: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof: [LibreSessionFlow-Claude-Code](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code)
- https://ormus.solutions

## License

MIT — see [LICENSE](./LICENSE).
