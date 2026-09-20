---
name: session-handoff
description: Write a clean session handoff for Grok Build. Use when ending a turn/session so the next agent or human can resume without archaeology.
---

# Session Handoff

Produce a handoff package others can pick up cold. The reader is future-you or a teammate with no memory of this turn. Git shows what changed. The handoff shows why, what was rejected, what looks wrong but is intentional, and the one next action.

Gold Hat: teach the *why* of each decision. A status report extracts attention; a baton that names the next edit and a verify command leaves the next person in control.

## When to use

- Ending a session with incomplete work (roughly > 30 minutes of state)
- Before sleep, machine switch, context-clear, or a gap longer than a few hours
- Handing a task to another human or another Grok Build turn
- Before you would otherwise say "I'll remember this tomorrow"

Do not use this skill for a one-shot that already shipped in the same turn. Do not use it as a changelog, PR body, or diary. After the package exists, run `continuity-checklist` (still a stub) as a smoke pass — call the stub; do not invent its depth. The reader-half of this contract is `session-pickup` (melted). Folding several sources into one block is `session-absorb` (melted).

## Operating steps

1. **Name the gap.** When will someone resume (later today, overnight, weekend, week+, teammate)? Same machine or not? This calibrates length. If unknown, assume overnight and say so.
2. **Name the job.** One or two sentences. Specific enough that a cold reader recognizes the mission.
3. **Mark the cursor.** File:line if mid-edit. Phase if mid-workflow. Failing test or hypothesis if mid-debug. Not "in progress."
4. **Split done / not done.** Done items need a path or a measurable claim. Not-done items name the remainder and the blocker if any.
5. **Write what the diff cannot show.** Decisions + why. False leads ("tried X, failed because Y"). Intentional oddities. What to read first.
6. **Pair every done claim with a verify.** A command or check the picker can run. Unverified "done" is a guess.
7. **Name one next action.** File, location, what to do. Then at most two follow-ons. "Continue" is a fail.
8. **Flag unknowns.** Do not invent state. Missing owner, missing blocker, missing path — write `unknown`.
9. **Teach one sentence.** Why this package is shaped this way, so the next writer can do it without you.

Stop if you cannot name the job or the next action. Ask. Inventing a next step is extraction.

## What belongs where

| Content | Goes in |
|---------|---------|
| File-by-file what changed | git log / diff — not the handoff |
| Why a decision was made | Handoff (ADR only if architectural) |
| False leads | Handoff |
| Open questions + blockers | Handoff |
| Customer-facing summary | PR description |
| Lessons that should outlive this task | Project docs / later absorb leftovers — not this file |
| Verify-still-done checks | Handoff |
| One specific next action | Handoff |

## Gap calibration

| Gap | Depth | Focus |
|-----|-------|-------|
| Same day, < 4 hours | Short | Next action + open questions |
| Overnight | Medium | Plus not-done + verify checks |
| Weekend | Fuller | Plus decisions + false leads |
| Week+ | Full | Plus references and project-level context |
| Month+ or teammate | Maximum | Treat the reader as new to the task |

Over-documenting a four-hour gap is noise. Under-documenting a vacation gap is archaeology.

## Pass / fail

| Check | Pass | Fail |
|-------|------|------|
| Job | Cold reader can say what the turn was for | "Made progress on the refactor" |
| Cursor | File:line, failing test, or named phase | "Still working on it" |
| Done vs not | Split; done items have paths or checks | One blob of "progress" |
| Diff-invisible | At least one why, false lead, or intentional oddity — or an explicit "none" | Restated `git log` |
| Verify | Each done claim has a command or check | "Trust me, tests pass" |
| Next action | One concrete edit or command | "Continue" / "finish the work" |
| Unknowns | Marked `unknown` or listed as questions | Invented owners, dates, or file paths |
| Secrets | None in the package | Tokens, keys, cookies, private URLs with credentials |
| Tone | Baton, not status report | "Today was productive. Looking forward to tomorrow." |

If a row would fail, fix the package before saving it. Do not ship a vibe handoff.

## Anti-patterns

**Status-report tone.** Future-you does not need morale. They need the next edit.

**Diff restatement.** "Changed `auth.ts` and updated tests" is git. "Null-check on `Session.refresh()` because expiry mid-flight; do not rip out retry — that broke the worker pool" is a handoff.

**Vague next step.** "Continue auth refactor" fails. "Replace `worker/pool.ts:91-145` with `TokenRefreshService.refresh()`; run `npm test worker`" passes.

**Skipped verify.** If you cannot name a check, the item is not done — move it to not-done or mark unverified.

**Wrong bin.** Do not dump a customer changelog or a durable architecture lesson here. Point at the PR or a doc.

## Worked example — overnight, mid-refactor

Job: share token refresh between CLI and worker. Gap: overnight, same machine.

Weak (fail):

```markdown
# Handoff
Productive session on auth. Tomorrow continue the refactor.
```

Stronger (pass):

```markdown
# HANDOFF — token-refresh-extract — 2026-09-20

## Job
Extract session refresh so CLI and worker share one retry path.

## Cursor
`worker/pool.ts:91` — inline refresh still present; new service exists, unused by the pool.

## Status
Done / blocked / next — **next** (not blocked).

## Done
- `auth/token-refresh.ts` — extracted service
- `auth/token-refresh.test.ts` — unit tests green in this turn
- CLI calls the service

## Not done
- Pool still inlines refresh at `worker/pool.ts:91-145`

## Decisions
- Direct import into the pool, not DI — pool constructs before the container (`pool.ts:78` attempt failed).

## False leads
- Tried constructor injection; broke startup order. Do not retry DI in this pass.

## Intentional oddities
- Retry/backoff copied from the old pool on purpose. Do not "clean it up" until both callers share tests.

## Open loops
| Loop | Owner | Blocker |
|------|-------|---------|
| Wire pool to service | next picker | none |

## Files touched
- `auth/token-refresh.ts` — new service
- `auth/token-refresh.test.ts` — coverage for extract
- CLI entry — switched caller
- `worker/pool.ts` — not finished

## Verify
```bash
npm test auth/token-refresh    # expect pass
rg -n "refreshToken" worker/pool.ts   # still hits; removal is the next edit
```

## Next 3
1. Replace `worker/pool.ts:91-145` with the service call; drop inline helpers.
2. Run `npm test worker`.
3. If green, delete the leftover imports.

## Unknowns
None.

## Teach
The next session should open at `pool.ts:91`, not by re-reading the extract. Verify before editing — "done" drifts.
```

That package is pickable: cursor, verify, one next edit. The weak version is not.

## Team or machine extras (only if true)

**Teammate.** Add why you are handing off, what to do first (read next action → key context → verify), and how to reach you. Do not invent a channel.

**Machine switch.** Note whether the branch is pushed, any local-only files, any machine-specific config. If unknown, write `unknown`.

**Mid-debug.** Do not put a fix you did not make. Put the current hypothesis, what you ruled out and why, and the next experiment.

## Output shape

```markdown
# HANDOFF — [task-slug] — [YYYY-MM-DD]

## Job
[1–2 sentences]

## Cursor
[file:line | phase | failing test / hypothesis]

## Status
done | blocked | next

## Done
- [claim + path]

## Not done
- [remainder + blocker if any]

## Decisions
- [choice] — [why]

## False leads
- Tried [X] — failed because [Y]

## Intentional oddities
- [looks wrong] — [why keep it]

## Open loops
| Loop | Owner | Blocker |
|------|-------|---------|
| … | … | … |

## Files touched
- [path] — [why]

## Verify
[commands / checks; one per done claim, or "unverified"]

## Next 3
1. [the one action — file + what]
2. …
3. …

## Unknowns
- [what you did not invent]

## Teach
[one reusable sentence]
```

Save where the next turn can find it (project `HANDOFF.md` is the default). Do not commit unless the user asked. Mention the path.

If nothing is incomplete and the work shipped, say so and skip the file. Empty theater handoffs are not allowed.

## Quality bar

A pass is done when a cold reader can run verify, open the cursor, and perform the first action without asking a question you already answered. Refuse vibe-only notes. Translate them or drop them.

Hand to `session-pickup` on resume. If several notes conflict, `session-absorb` first.

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Gold Hat: [GOLD_HAT.md](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/blob/main/GOLD_HAT.md). Sibling Libre*-Grok-Build packs: [README suite footer](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/blob/main/README.md).
