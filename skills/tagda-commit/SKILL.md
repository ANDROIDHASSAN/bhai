---
name: tagda-commit
description: "bhai's hardened mode for open-source contribution only. `/tagda-commit <repo link>` measures the repo's merge pattern, finds a real unclaimed bug, reproduces it, fixes it, proves it, and ends at a clean local commit ready for the user's yes to push — with the failure-mode checklist (branch before the first edit, diff holds only the fix and its test, every claim backed by a command, no trading a loud bug for a silent one) as a mandatory gate, not a self-check. Also handles 'raise N PRs today' / 'open source kar de pure din' / 'hit the daily target' by repeating this across repos until the count or the real candidates run out, not a fixed number per repo. Use when the user types /tagda-commit, says 'tagda commit', 'tagda commit kar de', or wants a hardened open-source contribution specifically — not a ticket or a from-scratch task."
---

# tagda-commit

`/bhai <repo link>`'s contribute route, run strict, and only that route — for when the ask is specifically open-source
contribution, not a ticket or a from-scratch build.

## 0. Which mode — one repo, or the daily grind?

**Names a repo, or "pick one and go"** → single-repo mode: just run §2 ("How to run it") once against that repo.

**No repo, and the ask is open-ended volume** ("open source kar de", "10 PRs raise kar de aaj", "pura din
contribute kar", "hit today's target") → **bulk mode**, §1 below.

**No repo, and the ask is a one-off with no volume signal** ("ek PR kholde", "kuch contribute kar") → ask one
short question and wait, don't guess or run anything yet:
- Already have a repo in mind? Give the link or `owner/repo`.
- Otherwise: what kind — a language, a domain (voice/ML/web/CLI...), or "koi bhi achi OSS repo" — and whether to
  pick from repos already forked/checked out in this workspace (if any exist here) or search fresh on GitHub for
  one with real outsider-PR merge activity.

If the input genuinely isn't asking for a contribution at all (a ticket, a from-scratch idea, a plain question),
say so and point to `/bhai`, `tagda-build`, or `tagda-explain` instead of asking the repo question.

## 1. Bulk mode — a daily total, not a per-repo number

The target (default 10 if the user didn't give a number) is a **total across however many repos it takes** — never
a fixed ceiling per repo. How many of those land in one repo is a judgment call from that repo's own measured merge
pattern, the same judgment a real top contributor uses, not a number pulled from the air:

- Don't open PR #2 in a repo while PR #1 there is unreviewed and the repo's own median time-to-merge hasn't passed
  yet. That's what actually hurts merge chance — not a count.
- A repo that reviews and merges fast and has a genuinely different, real, unclaimed bug for each slot can
  reasonably hold several of this account's PRs at once.
- A repo that's slow or clearly review-bandwidth-constrained: hold back there, move to the next repo instead of
  piling on.
- A repo's own ENFORCED policy still wins regardless of any of the above — one-PR-per-contributor, a required
  pre-assigned issue, an AI-contribution ban. That's the repo's rule, not this account's choice to override.

Loop: pick the next repo (prefer ones already forked/checked out here; survey fresh candidates only when those run
dry), run §"How to run it" against it, count a candidate that clears every hardened gate, move to the next repo.
Stop at the target, at running out of real candidates (report honestly — never lower the bar on one fix to hit a
number), or when the user says stop. Each candidate still gets its own local commit and its own explicit "yes"
before anything pushes — bulk mode changes how many repos get tried, not the push gate.

## 2. How to run it (one pass, single or bulk mode)

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
