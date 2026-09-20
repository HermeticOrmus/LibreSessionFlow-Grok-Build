# Contributing

## Melt, don't clone

Ports from LibreSessionFlow-Claude-Code must follow Liquid Gold:

1. Keep model-agnostic session handoff / pickup / absorb knowledge.
2. Strip Claude-only paths, `model:` pins, slash commands, `~/.claude/` memory, Anthropic install residue.
3. Ship as Grok `SKILL.md` / agents under `.grok/` conventions.
4. Teach while helping (Gold Hat).

## Skill format

```
skills/<name>/SKILL.md
```

YAML frontmatter: `name`, `description`.

A **melted** body needs: when to use, operating steps, pass/fail checks, one worked example, output shape, suite footer.

A **stub** is a short cue only. Do not mark it melted.

`skills/` is canonical. After editing a skill, copy it to `.grok/skills/<name>/SKILL.md` so dogfood matches.

## PR bar

- Honest depth: only count what you melt
- No "Grok killer" language
- No Claude plugin / agent / command totals as this repo's inventory
- Link Reality OS + sibling Libre*-Grok-Build packs in suite footers
