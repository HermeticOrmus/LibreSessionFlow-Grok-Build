---
name: thread-digest
description: "Stub, not a playbook. Summarize a Grok Build thread without losing actionable state. Use for long chats before handoff. No pack plugin digests a thread on its own; the nearest is the close plugin, grok plugin install close@libre-sessionflow-grok --trust."
---

# Thread Digest

Stub, not a playbook. No pack plugin digests a thread on its own. The nearest real depth is the [`close`](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code/tree/main/plugins/close) plugin from LibreSessionFlow-Claude-Code, whose session audit lists what was worked on, decisions, state and open threads. Install it from this marketplace: `grok plugin install close@libre-sessionflow-grok --trust`.

Status: **stub**, cue only. If several notes conflict, use melted `session-absorb`. See [docs/DEPTH_MATRIX.md](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/blob/main/docs/DEPTH_MATRIX.md).

Summarize for action, not for prose awards.

## Steps
1. Timeline of material turns only.
2. Outcomes (shipped / decided / blocked).
3. Actionable residue (todos, questions).
4. Drop chatter; keep citations to key messages if useful.
