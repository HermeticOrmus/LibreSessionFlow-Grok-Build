# Depth matrix

Update this table when melting. Status words mean what they say:

| Status | Meaning |
|--------|---------|
| stub | Thin cue only. Usable as a reminder, not a playbook. |
| melted | Real Grok skill: when-to-use, steps, measurable checks, example, output shape. |

Never copy Claude plugin / agent / command totals into this inventory. Upstream [LibreSessionFlow-Claude-Code](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code) is proof that the *job* exists, not a count this repo has earned.

| ID | Kind | Status | Source (Claude, for melt) | Notes |
|----|------|--------|---------------------------|-------|
| session-handoff | skill | melted | plugins/handoff (flagship) | Steps, pass/fail, overnight example. No `/handoff` theater. |
| session-pickup | skill | melted | plugins/pickup (shell + contract) | Reader-half: verify, stale-check, no re-ask. |
| session-absorb | skill | melted | plugins/absorb (shell) | Fold sources; conflict table. No `~/.claude/` memory backend. |
| context-pack | skill | stub | (adjacent compress job) | Teach-cue only. |
| continuity-checklist | skill | stub | plugins/close (adjacent) | Smoke list only. |
| thread-digest | skill | stub | (adjacent compress job) | Timeline cue only. |
| resume-plan | skill | stub | (adjacent after pickup) | Next-3 cue only. |
| session-orchestrator | agent | stub | (coordinator idea) | Coordinates the skills; not a melted specialist. |

This repo now: **3 melted skills**, **4 stub skills**, **1 stub agent**.

Where they live: melted skills in `plugins/libre-sessionflow-grok/skills/<name>/SKILL.md` (the plugin installs them); stubs in `stubs/<name>/SKILL.md` (nothing installs them); the agent in `AGENTS/session-orchestrator.md`.

Dogfood copies of every skill live at `.grok/skills/<name>/SKILL.md` and must match the canonical file above. CI checks it.

## Pack entries (installed, not melted)

The marketplace also lists every plugin of [LibreSessionFlow-Claude-Code](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code) as a remote entry: **10 entries**, all pinned to one pack commit (the `sha` in `.grok-plugin/marketplace.json`). Grok reads those plugin folders as they are. They are not counted in the melted inventory above. `scripts/pin-pack.sh` re-pins them; CI fails when the pack gains or loses a plugin.

Nearest pack plugin per stub: `continuity-checklist` to `close` (real depth), `context-pack` to `handoff`, `thread-digest` to `close`, `resume-plan` to `pickup` (nearest only; no pack plugin does those three jobs one to one). Details: [stubs/README.md](../stubs/README.md).

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Sibling Libre*-Grok-Build packs: [README suite footer](../README.md).
