# Contributing

## Ways to contribute

- **Seal a crack.** [LEDGER.md](./LEDGER.md) lists the open cracks with their evidence and the seal each one needs. Pick an `open` row, prove it with a failing check where you can, fix it, and set the row to `sealed` with your PR number.
- **Melt a pack skill into a Grok-native one.** Take a stub from [stubs/](./stubs/) or a skill from a [LibreSessionFlow-Claude-Code](https://github.com/HermeticOrmus/LibreSessionFlow-Claude-Code) plugin and write it to the melted bar below. The steps are in [stubs/README.md](./stubs/README.md#melt-a-stub).
- **Report a routing miss.** When Grok picks the wrong skill, or none, the description is what needs fixing: [routing miss form](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/issues/new?template=routing-miss.yml).
- **Propose a plugin.** Name a real job, what Grok gets wrong today without it, and a check anyone can run: [plugin proposal form](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/issues/new?template=plugin-proposal.yml).

General feedback goes in the [feedback form](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/issues/new?template=feedback.yml).

## Melt, don't clone

Ports from LibreSessionFlow-Claude-Code must follow Liquid Gold:

1. Keep model-agnostic session handoff / pickup / absorb knowledge.
2. Strip Claude-only paths, `model:` pins, slash commands, `~/.claude/` memory, Anthropic install residue.
3. Ship as Grok `SKILL.md` / agents under `.grok/` conventions.
4. Teach while helping (Gold Hat).

## Skill format

```text
plugins/libre-sessionflow-grok/skills/<name>/SKILL.md   # melted
stubs/<name>/SKILL.md                                   # stub
```

YAML frontmatter: `name`, `description`. The description is the routing line Grok reads: say what the skill does and when to use it (`Use when ...`).

A **melted** body needs: when to use, operating steps, pass/fail checks, one worked example, output shape, suite footer.

A **stub** is a short cue only. Do not mark it melted. It lives in `stubs/`, never in the plugin, and names the pack plugin nearest to the real depth.

`plugins/libre-sessionflow-grok/skills/` (melted) and `stubs/` (stubs) are canonical. After editing a skill, copy it to `.grok/skills/<name>/SKILL.md` so dogfood matches; CI checks it.

Before you name a new skill, check the pack's skill names: two installed plugins with a skill of the same name give Grok two skills with one name (see K-09 in the ledger).

## PR bar

- Honest depth: only count what you melt
- No "Grok killer" language
- No Claude plugin / agent / command totals as this repo's inventory
- Link Reality OS + sibling Libre*-Grok-Build packs in suite footers
- `grok plugin validate plugins/libre-sessionflow-grok` passes; CI runs it, checks the pack pins, and installs every marketplace entry into a clean Grok home
- When the pack adds or drops a plugin, CI fails and says so: run `scripts/pin-pack.sh`, commit `.grok-plugin/marketplace.json`, and update the Depth table if the count changed
