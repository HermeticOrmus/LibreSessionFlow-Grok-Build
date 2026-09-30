---
name: session-absorb
description: Fold prior thread or handoff state into the current Grok Build turn. Use when context is scattered across messages or digests.
---

# Session Absorb

Integrate prior state into the active turn. Absorb is a merge, not a memoir. Several notes become one block the current turn can trust.

Gold Hat: show what you dropped and why. Silent overwrite extracts the user's memory. An explicit keep / drop / conflict list leaves them able to judge the merge.

This skill is **not** Claude project-memory and does not write `~/.claude/`. Durable cross-task lessons belong in the repo's own docs when the user asks — leftover, not a fake absorb backend.

## When to use

- Context is split across a handoff, a thread digest, chat messages, and/or a context-pack
- Two sources disagree (goal, decision, next action)
- Pickup would otherwise guess which note is canonical
- Mid-turn, after a long thread, before you write the next handoff

Use `thread-digest` or `context-pack` (both still stubs) to compress a single source first if the raw thread is huge — call the stubs; do not invent a novel. Use `session-pickup` when there is **one** trusted handoff. Use `session-handoff` to persist the absorbed block at the end of the turn.

Do not absorb when a single current handoff is enough. Do not use absorb to hide conflicts.

## Operating steps

1. **Collect sources.** List each artifact: path, date (or `unknown`), and kind (handoff, digest, message, pack). If you cannot find a source the user named, say missing — do not hallucinate its contents.
2. **Extract fields, do not paraphrase yet.** Goals, decisions, open loops, constraints, next actions, verify claims. Keep the source tag on each item.
3. **Deduplicate.** Same decision stated twice → keep the newer dated one, or the one with a why. Note the collapse.
4. **Mark conflicts explicitly.** Same field, incompatible values. Do not average them. Do not pick silently. Table: field, source A, source B, resolution (user / newer / `unresolved`).
5. **Drop with a reason.** Chatter, restated git, superseded next-actions, secrets. Every drop gets a one-line why.
6. **Emit one absorbed block** in the output shape below. One job, one cursor if known, ranked loops, leftover unknowns.
7. **State trust.** Which source is canonical for the next action. If unresolved conflict touches that action, stop and ask.

Stop if sources are missing or a conflict blocks the first action. Asking is cheaper than a silent wrong merge.

## Keep / drop / conflict

| Kind | Keep | Drop | Conflict |
|------|------|------|----------|
| Goal | Current must-goals | Nice-to-haves already shipped or rejected | Two different primary jobs |
| Decision + why | Dated decision with rationale | Decision restated without why (keep the one with why) | Opposite choices, both still claimed |
| Open loop | Ranked, with owner/blocker or `unknown` | Loops marked done in a newer source | Same loop, different blockers |
| Next action | The one that matches the surviving cursor | Older "next" superseded by a later handoff | Two first actions that cannot both be first |
| Verify | Commands still claimed | Checks for files that no longer exist (move to stale) | Same claim, opposite expected results |
| Secret | Never keep in the block | Always drop; say "secret omitted" | — |

## Pass / fail

| Check | Pass | Fail |
|-------|------|------|
| Source list | Every input named; missing marked missing | "From context" with no list |
| Dedup | Collapsed repeats, tagged | Same decision three times as if new |
| Conflicts | Table, unresolved if truly unresolved | Silent pick, or "merged the vibes" |
| Drops | Each drop has a why | Content vanished with no note |
| Single job | One primary job in the block | Two missions left co-equal |
| Next action | One first action, or stop+ask | Two first actions |
| Secrets | Omitted | Tokens copied "for completeness" |
| Honesty | Stub leftovers named as stubs | Pretend `thread-digest` was a full melt |

Unresolved conflicts that do **not** touch the first action may stay listed. Unresolved conflicts that **do** touch it fail the absorb until the user chooses.

## Anti-patterns

**Memoir.** A narrative of the week is a digest leftover, not an absorb. Cut to fields.

**Silent winner.** Picking the friendliest next action when two handoffs disagree.

**Re-expansion.** Absorb is smaller than the union of sources. If the block is longer than the inputs, you failed to drop.

**Memory theater.** Do not claim you wrote durable memory to a Claude path. If the user wants a standing note, write a repo doc they asked for.

## Worked example — handoff vs digest

Sources:

1. `./HANDOFF.md` (2026-09-19) — next action: wire `worker/pool.ts` to `TokenRefreshService`; decision: no DI this pass.
2. Thread digest (2026-09-20, stub-quality notes) — next action: "revisit DI"; mentions a failing `npm test worker` after an unrelated merge; also pastes a sample token (drop).

Weak absorb (fail): "We'll look at DI and the pool. Tests might be fine."

Stronger absorb (pass):

```markdown
## Sources
- `./HANDOFF.md` — 2026-09-19 — handoff
- thread digest — 2026-09-20 — digest (stub compression; treat as hints)

## Job
Share token refresh between CLI and worker.

## Conflicts
| Field | A (handoff 19th) | B (digest 20th) | Resolution |
|-------|------------------|-----------------|------------|
| Next action | Wire pool; no DI | Revisit DI | **unresolved** — blocks first action |
| Worker tests | not mentioned | claimed red after merge | take B as unverified warning |

## Kept
- Cursor candidate: `worker/pool.ts` inline refresh
- Decision (19th): direct import, not DI — still in force unless user overturns it
- Open loop: wire pool

## Dropped
- Digest "revisit DI" as a *silent* replacement — it contradicts the handoff; not dropped as a conflict row
- Sample token in digest — secret omitted
- Digest chatter / restated git

## Absorbed context
Status: **blocked on conflict** (DI vs wire-pool-as-written).
Verify to run after the user chooses: `npm test worker` (digest says red; unverified).

## Trust
Handoff is canonical for the extract decision. Digest is newer for test-health but unverified.
Not starting either edit until the user picks: (1) keep no-DI and wire the pool, or (2) reopen DI with a new why.

## Teach
Newer is not automatically righter. A digest that flips a decision without a why is a conflict, not a win.
```

After the user picks (1), rewrite the Next action to the pool edit and proceed to `session-pickup` on the absorbed block.

## Output shape

```markdown
## Sources
- [path or label] — [date or unknown] — [kind]
- [missing: …]

## Job
[one primary job]

## Conflicts
| Field | Source A | Source B | Resolution |
|-------|----------|----------|------------|
| … | … | … | user / newer / unresolved |

## Kept
- [field] — [value] — from [source]

## Dropped
- [item] — [why]

## Absorbed context
### Status
done | blocked | next

### Decisions
- [choice] — [why] — [source]

### Open loops
| Loop | Owner | Blocker | Source |
|------|-------|---------|--------|
| … | … | … | … |

### Verify (from sources)
- [check] — claimed by [source] — not yet run | stale

### Next action
[one action] — or **stop: unresolved conflict on [field]**

## Trust
[which source is canonical for the first action]

## Teach
[one reusable sentence]
```

If there is only one source and no conflict, say so and point at `session-pickup` instead of performing theater.

## Quality bar

A pass is done when a picker can act on one job and one next action (or knows exactly which conflict to ask about), and can see every drop. Refuse a merge that "just combines everything."

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Gold Hat: [GOLD_HAT.md](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/blob/main/GOLD_HAT.md). Sibling Libre*-Grok-Build packs: [README suite footer](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/blob/main/README.md).
