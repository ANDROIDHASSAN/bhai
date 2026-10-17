---
name: bhai-audit
description: "Scans one or more repos for real, unclaimed contribution opportunities and reports a ranked list — finds candidates, fixes nothing, opens nothing. Use when the user says /bhai-audit, 'bhai audit kar de', 'kahan contribute kar sakte he', or wants to know what's worth fixing before committing to any one of them, across one repo or several."
---

# bhai-audit

`/bhai <repo>`'s measure-and-find steps, without the fix. For when the user wants to see what's out there before
picking one — scanning several repos is cheap; writing a fix in each is not.

## Steps

For each repo named (or, with no name given, every repo the user already has a fork/checkout for):

1. `../bhai/skills/bhai/references/route-contribute.md` §1 (measure the merge pattern and AI-contribution policy)
   and §2 (find a real bug — quickstart/examples with edge inputs, then unclaimed issues, then code-reading leads
   that still need a runnable reproduction before they count). Stop at a candidate; don't fix it.
2. For each candidate found: one line on what's wrong, how it reproduces, and why it's unclaimed (checked
   `gh search prs`/open issues yourself — don't just assume).
3. Rank by the repo's own measured merge pattern: a repo that merges outsider PRs in hours and has open slots
   ranks above one that's slow, review-bandwidth-constrained, or already at a de facto cap for this account.

## Report

```
<repo> — <N candidate(s) found / nothing solid>
  1. <one line: the bug, how it reproduces, why it's unclaimed>
  2. ...
Best bet: <repo + candidate>, because <merge speed / open slot / how solid the repro is>
```

No code is written, no branch created, nothing committed. If the user wants one of these built out, that's a
separate `/bhai <repo>` or `/tagda-commit <repo>` run — tell them which candidate to point it at.
