---
name: tagda-fix
description: "bhai's hardened mode — any route. `/tagda-fix <repo link>` finds a real bug and prepares a merge-worthy PR; `/tagda-fix <ticket link or key>` solves the ticket end to end; `/tagda-fix <anything else>` does the task — exactly like /bhai, except the failure-mode checklist (branch before the first edit, diff holds only the fix and its test, every claim backed by a command, no trading a loud bug for a silent one) is a mandatory gate instead of a self-check, and the reply names which checks ran. For open-source contribution specifically, prefer the narrower `tagda-commit` sibling. Use when the user types /tagda-fix, says 'tagda fix', 'tagda fix kar de', or asks for a solid/robust/hardened fix, a ticket, or a task — and wants bhai's extra-strict pass, not the regular one."
---

# tagda-fix

`/bhai` run strict. Same engineer, same routing, same spine — this skill just refuses to let four specific mistakes
slide, because they are the ones measured to actually happen on a fast or distracted pass:

1. A commit landing on the default branch instead of a feature branch.
2. The diff drifting into unrelated reformatting, deleted lines, or a stray scratch file.
3. A claim ("tested X", "version bumped", "committed") with no command in this session backing it.
4. A fix that trades a loud bug for a silent one (a `try/except` that hides a crash by quietly returning the
   wrong thing instead of fixing why the call failed).

## How to run it

1. Load `../bhai/SKILL.md` and follow it exactly — same route table, same spine, same hard rules, same references
   (`../bhai/references/*.md`). Nothing here replaces that; this skill only tightens what was already optional.
2. Treat `../bhai/references/fix-quality.md` §8 ("Failure modes measured on free-tier backends") as **mandatory
   gates**, checked in order, not a self-review pass:
   - `git branch --show-current` is not `main`/`master`/`trunk` — checked before the first edit, not after.
   - `git diff <base> --stat`, pasted, shows only the fix and its test (plus a changelog fragment/version bump
     only where the repo's own rules require it). Anything else gets cleaned up and the stat re-run.
   - Every claim in the report traces to a command run in this session; if you can't point to the command, the
     claim doesn't go in.
   - A fallback/except path that avoids a crash is checked for what it does to the caller: if it silently drops
     data or returns a plausible-but-wrong result, that's not accepted as the fix — find the real cause or make
     the failure visible instead.
3. If any one of these would fail, **stop and say which one** rather than reporting done — that's the entire
   difference from the plain route: a failing hardened gate is a blocker here, not a note for later.
4. Tag the mode everywhere `/bhai` would show its route line or explanation:
   - Route line: *"Route: contribute · mode: tagda fix · symptom: X · done when: Y"*.
   - In `explain.md`'s format, add one line before "Tumhe karna hai": `Hardened: <which checks ran and confirmed,
     in a few words>`.

## When not to reach for this

If the task is read-only (status, a question, exploring a repo) there is nothing to harden — just load `/bhai`
directly; `tagda-fix`'s extra gates only bite once there is a diff to check. Open-source contribution specifically
→ `tagda-commit`. A question with no code change → `tagda-explain`. Building a real thing from a rough idea,
not a small change to existing code → `tagda-build`.
