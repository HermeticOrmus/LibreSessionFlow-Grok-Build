# LibreSessionFlow-Grok-Build

**Session handoff, pickup, and absorb for [Grok Build](https://github.com/HermeticOrmus/grok-build-reality-os)** — ported and melted from [LibreSessionFlow-Claude-Code](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code), not a dumb copy.

> Status: **v0 public scaffold** — honest stubs. Melt depth next.

## Why this exists

Long agent sessions lose context. SessionFlow owns handoff / pickup / absorb patterns so the next turn (or next human) can resume without archaeology. Grok Build needs the same *job* with Grok-native skills, agents, `.grok/`, and truth-seeking voice.

## Install (<5 min)

See [QUICK_START.md](./QUICK_START.md).

```bash
mkdir -p .grok/skills
cp -R skills/* .grok/skills/
```

Doctrine: install [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine first.

## Depth matrix (honest)

| Artifact | v0 scaffold | Upstream Claude (proof) |
|----------|-------------|-------------------------|
| Skills (melted bodies) | 7 stubs → fill next | see upstream suite |
| Agents | 1 (`session-orchestrator`) | upstream agents |

Counts on the right are **upstream proof**, not this repo's claim until melted.

## First skills

| Skill | Job |
|-------|-----|
| session-handoff | Write a clean handoff package for the next agent/human |
| session-pickup | Resume from a handoff with minimal re-discovery |
| session-absorb | Fold prior thread state into current work |
| context-pack | Compress goals, decisions, open loops into a pack |
| continuity-checklist | Smoke checks before ending a session |
| thread-digest | Summarize a thread without losing actionable state |
| resume-plan | Produce a next-3-actions resume plan |

Agent: `AGENTS/session-orchestrator.md` — full continuity pass.

## Layout (Grok Build)

```
skills/                 # install into .grok/skills or ~/.grok/skills
AGENTS/                 # suite agents
.grok/plugins/          # optional plugin bundle
docs/                   # DEPTH_MATRIX, MELT_RULES
```

## Gold Hat

[GOLD_HAT.md](./GOLD_HAT.md) — empower or extract?

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- Sibling: [LibreUIUX-Grok-Build](https://github.com/HermeticOrmus/LibreUIUX-Grok-Build)
- Skills packs: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof: [LibreSessionFlow-Claude-Code](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code)
- https://ormus.solutions

## License

MIT — see [LICENSE](./LICENSE).
