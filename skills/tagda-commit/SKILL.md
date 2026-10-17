---
name: tagda-commit
description: "bhai's hardened mode for open-source contribution only. `/tagda-commit <repo link>` measures the repo's merge pattern, finds a real unclaimed bug, reproduces it, fixes it, proves it, and ends at a clean local commit ready for the user's yes to push — with the failure-mode checklist (branch before the first edit, diff holds only the fix and its test, every claim backed by a command, no trading a loud bug for a silent one) as a mandatory gate, not a self-check. Use when the user types /tagda-commit, says 'tagda commit', 'tagda commit kar de', or wants a hardened open-source contribution specifically — not a ticket or a from-scratch task."
---

# tagda-commit

`/bhai <repo link>`'s contribute route, run strict, and only that route — for when the ask is specifically open-source
contribution, not a ticket or a from-scratch build. If the input isn't a repo link or `owner/repo`, say so and point
to `/bhai` (routes anything) or `tagda-fix` (hardened, any route) instead.

## How to run it

1. Load `../bhai/skills/bhai/references/route-contribute.md` and follow it exactly — measure the repo, find a real
   unclaimed bug, fix and prove it, draft the PR. Nothing here replaces that.
2. Treat `../bhai/skills/bhai/references/fix-quality.md` §8 as **mandatory gates**, checked in this order, before
   the commit:
   - `git branch --show-current` is not `main`/`master`/`trunk` — branch first, before the first edit.
   - `git diff <base> --stat`, pasted, shows only the fix and its test (plus a changelog fragment/version bump
     only where the repo's own rules require it). Clean up and re-run the stat if anything else is there.
   - Every claim in the report ("fails on main", "tests pass", "committed") traces to a command run in this
     session.
   - Any fallback/except path added by the fix is checked for what it does to the caller — a silent wrong result
     is not accepted in place of the crash it replaces.
3. If any gate would fail, **stop and say which one** instead of reporting a candidate as ready.
4. Route line: *"Route: contribute · mode: tagda commit · symptom: X · done when: Y"*. Explanation: `explain.md`'s
   format plus the `Hardened:` line.
5. Stop at the local commit — push and PR-open still need the user's explicit yes in this session, same as `/bhai`.

## When not to reach for this

A ticket or a from-scratch task → `tagda-fix` (same hardening, any route). A plain question → `tagda-explain`.
