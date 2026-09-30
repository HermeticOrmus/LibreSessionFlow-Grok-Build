# Stubs

A stub is a thin cue: a name, a one-line job, and a few steps or checks. It is a reminder, not a playbook, so nothing here installs. Each stub names the pack plugin nearest to the real depth, and that plugin installs from this repo's marketplace. Where no pack plugin does the stub's job one to one, the stub says so and names the nearest.

| Stub | Job | Pack plugin | Fit | Install |
|------|-----|-------------|-----|---------|
| [continuity-checklist](./continuity-checklist/SKILL.md) | End-of-session smoke | [`close`](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code/tree/main/plugins/close) | real depth: the end-of-session ritual | `grok plugin install close@libre-sessionflow-grok --trust` |
| [context-pack](./context-pack/SKILL.md) | Compress goals, decisions, open loops | [`handoff`](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code/tree/main/plugins/handoff) | nearest: writes state, decisions and open loops into a HANDOFF.md | `grok plugin install handoff@libre-sessionflow-grok --trust` |
| [thread-digest](./thread-digest/SKILL.md) | Summarize a thread for action | [`close`](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code/tree/main/plugins/close) | nearest: its session audit lists work, decisions, state, open threads | `grok plugin install close@libre-sessionflow-grok --trust` |
| [resume-plan](./resume-plan/SKILL.md) | Next 3 actions after pickup | [`pickup`](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code/tree/main/plugins/pickup) | nearest: re-runs verify and shows the next action | `grok plugin install pickup@libre-sessionflow-grok --trust` |

Also here: [libresessionflow-core/](./libresessionflow-core/), the v0 plugin bundle stub. It had no manifest and installed only a copy of the stub orchestrator. It is kept as the record; [plugins/libre-sessionflow-grok](../plugins/libre-sessionflow-grok/) replaces it.

The suite agent [AGENTS/session-orchestrator.md](../AGENTS/session-orchestrator.md) is also a stub coordinator. It stays where [AGENTS.md](../AGENTS.md) points, and nothing installs it: you merge it by hand.

## Melt a stub

1. Write the skill to the melted bar in [CONTRIBUTING.md](../CONTRIBUTING.md#skill-format): when to use, operating steps, pass/fail checks, one worked example, output shape, suite footer.
2. `git mv stubs/<name> plugins/libre-sessionflow-grok/skills/<name>`, drop the stub lines, and give the frontmatter a routing description (`Use when ...`).
3. Copy it to `.grok/skills/<name>/SKILL.md` (CI checks the copy matches).
4. Update [docs/DEPTH_MATRIX.md](../docs/DEPTH_MATRIX.md), this table, and the README skills table.

The dogfood copies of these stubs in `.grok/skills/` match the files here, so a session opened in this repo sees them described as stubs.
