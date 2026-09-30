---
name: session-pickup
description: Resume work from a prior handoff for Grok Build. Use when starting a turn that should continue previous session state.
---

# Session Pickup

Resume from a handoff with minimal re-discovery. You are the reader-half of the handoff contract: verify, then act. Do not re-explore a solved tree.

Gold Hat: teach which questions are already closed. Re-asking solved questions extracts the user's time. Confirming a stale path and naming the first real action leaves them in control.

## When to use

- Starting a turn that should continue a previous session
- A `HANDOFF.md` (or equivalent package) exists and names a next action
- After a gap: sleep, machine switch, context-clear, teammate baton

Use `session-handoff` first if there is no package — do not invent one from vibes and call it pickup. Use `session-absorb` (melted) when several digests, messages, or handoffs disagree. Use `resume-plan` (still a stub) only after pickup has a verified cursor; call the stub, do not invent a three-week program.

Do not use this skill to start greenfield work. Do not treat pickup as a second handoff write.

## Operating steps

1. **Find the package.** Default: project `HANDOFF.md`. If several exist, ask which task or absorb first. If none exist, stop and say so.
2. **Read once for the job, twice for key context.** Job, cursor, done / not done, decisions, false leads, next action, unknowns. Do not skim past "intentional oddities."
3. **Stale-check before you trust it.** Paths still exist? Branch still the one named? APIs or decisions reversed in git since the handoff date? Mark each: current / stale / unverified.
4. **Run verify.** Execute the handoff's checks (or the closest equivalent). Record pass / fail / could-not-run. A failed verify is a finding, not optional color.
5. **Confirm or revise the next action.** If verify passed and the cursor is current, take the named first action. If stale or failed, say what changed and propose a revised first action — do not silently rewrite history.
6. **Ask only for missing blockers.** Owner, secret, access, or a decision the handoff listed as open. Do not re-ask questions the handoff already answered.
7. **State the first move.** File + what you will do now. Then do it (or wait if the user must confirm a revised plan).
8. **Update continuity as you go.** When the cursor moves, note it. End-of-turn write belongs to `session-handoff`, not a shadow diary here.

Stop if the package is missing, unreadable, or so stale that verify cannot even be attempted. Say what you need. Guessing the mission is extraction.

## The contract (handoff writes, pickup reads)

| Handoff field | Pickup duty |
|---------------|-------------|
| Done | Run verify; mark still-done or drifted |
| Not done / open loops | Pick the top loop unless the user names another |
| Key context / false leads | Read before any edit; do not retry a ruled-out path without new evidence |
| Next action | Confirm or revise in the open |
| Unknowns / open questions | Resolve with the user or carry forward — do not fill with fiction |
| Verify commands | Run them (or say you could not) |

## Pass / fail

| Check | Pass | Fail |
|-------|------|------|
| Source | Named the handoff path (or said none exists) | "I recalled the context" with no artifact |
| Job restated | One line, from the package | New mission invented |
| Stale-check | Each critical path/decision marked current, stale, or unverified | Assumed yesterday is still true |
| Verify | Results recorded (pass / fail / could-not-run) | Skipped because "it should be fine" |
| Next action | Confirmed or revised with a reason | Ignored the named step and started a tour |
| Questions | Only blockers the package does not answer | Re-asked solved decisions |
| False leads | Not retried without new evidence | "Let me try DI again" after the handoff forbade it |
| Secrets | None echoed from the package | Pasted tokens into the new turn |
| Tone | Resume, not a recap essay | Multi-page restatement of the handoff |

If verify failed, pickup is not blocked forever — it is **revised**. Say drift, then the new first action.

## Anti-patterns

**Archaeology tour.** Re-reading the whole repo "to be safe" after a complete handoff wastes the package. Open the cursor.

**Silent revision.** Changing the next action without saying the handoff was stale hides the truth from the user.

**Re-asking.** "Should we extract refresh into a service?" when the handoff says that decision is done.

**Skipping verify.** State drifts. The file you "finished" may have been reverted.

**Pickup-as-handoff.** Do not write a new `HANDOFF.md` at the start unless the old one is wrong and you are correcting it in the open.

## Worked example — overnight resume

Package (abridged) from `./HANDOFF.md`:

```markdown
## Job
Extract session refresh so CLI and worker share one retry path.

## Cursor
`worker/pool.ts:91` — service exists, pool still inline.

## Verify
npm test auth/token-refresh    # expect pass

## Next 3
1. Replace `worker/pool.ts:91-145` with the service call.
```

Weak pickup (fail): "I'll look around the auth folder and see where we are. Should we extract a service?"

Stronger pickup (pass):

```markdown
## Source
`./HANDOFF.md` — token-refresh-extract — 2026-09-20

## Job
Share token refresh between CLI and worker. Primary action: wire the pool.

## Stale-check
- `worker/pool.ts` — current (file exists; inline refresh still at ~91)
- `auth/token-refresh.ts` — current
- Decision "no DI this pass" — current (no contrary commit)

## Verify
- `npm test auth/token-refresh` — pass (47)
- `rg -n "refreshToken" worker/pool.ts` — hits remain (matches "not done")

## Next action
Confirmed: replace `worker/pool.ts:91-145` with `TokenRefreshService.refresh()`.
Not asking whether to extract — that is already decided.

## Questions
None. No missing blocker.

## First move
Edit `worker/pool.ts:91-145` now.
```

If verify had failed (`token-refresh` tests red), the pass would instead say: **revised** — tests drifted; inspect the failure before touching the pool; do not wire a red service.

## Output shape

```markdown
## Source
[path] — [slug] — [date]  (or: none found)

## Job
[from the package, one line]

## Stale-check
- [path or decision] — current | stale | unverified — [note]

## Verify
- [check] — pass | fail | could-not-run — [evidence]

## Next action
confirmed | revised — [the one action]
[if revised: what drifted and why this action instead]

## Questions
- [only missing blockers]
  (or: none)

## First move
[file + what you will do in this turn]
```

If the handoff is excellent and verify is green, keep this block short. Length is not quality. A cold start that ignores the package is a fail even if the prose is tidy.

## Quality bar

A pass is done when the first edit matches a verified cursor and no solved question was re-asked. If you cannot verify, say so and pick the smallest action that restores a known state.

When several sources conflict, stop and run `session-absorb`. When the turn ends, run `session-handoff`.

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Gold Hat: [GOLD_HAT.md](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/blob/main/GOLD_HAT.md). Sibling Libre*-Grok-Build packs: [README suite footer](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build/blob/main/README.md).
