# Quick Start — LibreSessionFlow for Grok Build

> From zero to a clean handoff in under 5 minutes.

## Prerequisites

- Grok Build installed and working
- An active or ending agent session

## Install skills (repo-local)

```bash
git clone https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build.git
cd your-project
mkdir -p .grok/skills
cp -R /path/to/LibreSessionFlow-Grok-Build/skills/* .grok/skills/
```

Or user-global:

```bash
mkdir -p ~/.grok/skills
cp -R /path/to/LibreSessionFlow-Grok-Build/skills/* ~/.grok/skills/
```

## First-run teach cue

1. **Handoff** — "Run session-handoff: goals, decisions, open loops, files touched, next 3 actions."
2. **Pickup** — "Run session-pickup on that handoff and continue the top open loop."
3. **Absorb** — "Run session-absorb to fold prior thread digest into this turn."

## Smoke checklist

- [ ] Skills visible to Grok
- [ ] One handoff produced with measurable sections
- [ ] One pickup resumed without re-asking solved questions
