---
name: context-pack
description: "Stub, not a playbook. Compress goals, decisions, and open loops into a portable context pack for Grok Build sessions. No pack plugin makes a standalone context pack; the nearest is the handoff plugin, grok plugin install handoff@libre-sessionflow-grok --trust."
---

# Context Pack

Stub, not a playbook. No pack plugin makes a standalone context pack. The nearest real depth is the [`handoff`](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code/tree/main/plugins/handoff) plugin from LibreSessionFlow-Claude-Code, which writes state, decisions and open loops into a HANDOFF.md. Install it from this marketplace: `grok plugin install handoff@libre-sessionflow-grok --trust`.

Status: **stub**, cue only. For a usable playbook use melted `session-handoff` / `session-absorb`. See [docs/DEPTH_MATRIX.md](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/blob/main/docs/DEPTH_MATRIX.md).

Compress session state into a portable pack.

## Steps
1. Goals (must / should / nice).
2. Decisions + rationale (short).
3. Open loops ranked by severity.
4. Constraints and non-goals.
5. Keep under a scannable length; link out for detail.
