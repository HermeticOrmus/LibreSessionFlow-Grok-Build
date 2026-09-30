# libre-sessionflow-grok

The Grok-native LibreSessionFlow plugin. It carries the skills melted for Grok Build, and only those:

| Skill | Job | Melted from (pack plugin) |
|-------|-----|---------------------------|
| `session-handoff` | Write a handoff package a cold reader can pick up | `handoff` |
| `session-pickup` | Resume from a handoff: stale-check, verify, confirm the next action | `pickup` |
| `session-absorb` | Fold scattered sources into one block; table the conflicts | `absorb` |

Install:

```bash
grok plugin marketplace add HermeticOrmus/LibreSessionFlow-Grok-Build
grok plugin install libre-sessionflow-grok@libre-sessionflow-grok --trust
```

These skills write to the project (a `HANDOFF.md` by default) and never to a Claude memory path. The pack's `pickup` plugin also ships a skill named `session-pickup`; install one of the two, or see [LEDGER.md](../../LEDGER.md) for the open crack.

The four stub skills are not in this plugin. They live in [stubs/](../../stubs/), and each names the pack plugin nearest to the real depth. The same marketplace installs those pack plugins.

Manifest: [.grok-plugin/plugin.json](./.grok-plugin/plugin.json). Honest inventory: [docs/DEPTH_MATRIX.md](../../docs/DEPTH_MATRIX.md). The v0 bundle stub this plugin replaces is kept at [stubs/libresessionflow-core/](../../stubs/libresessionflow-core/).
