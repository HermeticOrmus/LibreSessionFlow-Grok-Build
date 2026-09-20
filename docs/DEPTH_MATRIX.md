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

Dogfood copies of every skill live at `.grok/skills/<name>/SKILL.md` and must match `skills/<name>/SKILL.md`.

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Sibling Libre*-Grok-Build packs: [README suite footer](../README.md).
