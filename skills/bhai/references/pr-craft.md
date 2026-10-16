# PR craft

The maintainer must see three things in under two minutes: the bug is real, the fix is the smallest correct one,
and nothing else changed. Everything here serves those three.

## Before the PR exists
- **Capacity**: at most 2 open PRs from the user per repo (3 only where the user already has merges there).
- **Unclaimed**: no open PR, no "I'll take this" comment, no assignee on the issue. New issues attract competing PRs
  within hours; if the fix is ready, open it promptly once the user says yes.
- **Issue first** only when the repo requires it or the change is a feature. A self-found bug with a full reproduction
  can go straight to a PR. For a bug with real user impact, an issue (mechanism, runnable repro, observed vs expected,
  versions) plus the PR with `Fixes #N` is strongest; have the PR ready before filing so both land within minutes.

## Title
Use the style the repo's merged outsider PRs use (`merge-readiness.md`): conventional `type(scope): lowercase
imperative` with the scope from the file's own git history, or a plain sentence about the user-visible effect.
At most ~75 characters. The title is the commit subject.

## Body (the repo's template wins; otherwise this)
```
<Problem: what goes wrong, for whom, with the smallest runnable reproduction and the observed output.>

<Fix: what changed and why this is the smallest correct place for it.>

Tests: <new test name(s); "fails on main with <quoted error>"; the repo's checks that passed, quoted counts.>

Not changed: <real but out-of-scope findings, so the reviewer sees you saw them.>
```
Plain prose, no marketing words, no emoji, no "comprehensive", no headings for a small fix. Every number and every
"fails on main" comes from a command in this run; update the body in the same run when a later commit changes it.

## Commits
One commit per logical change; conventional subject if the repo uses it; body says why. Sign-off (`-s`) where DCO is
required. Only the user's identity. Never force-push an open PR: add commits; resolve conflicts by merging the
default branch into the PR branch.

## Pre-flight (answer from this run's output)
1. Does the new test fail on the default branch, each assertion on its own?
2. Did the repo's lint, format, type and test commands pass on this exact commit?
3. Is every claim in the body something that was run?
4. Does `git diff <base> --stat` show only the fix and its test (plus required fragments)?
5. Title in the repo's style, ≤ ~75 characters?
6. Capacity still respected after this PR?
7. Commit author is the user, with their noreply email if they use one?

## Reviews
- Read every bot comment in full. Right → fix with a test in a new commit, reply on that thread naming the commit.
  Wrong → reply once with evidence. On a trade-off the bot keeps flipping, check the default branch and official docs
  once, pick, document, and stop; never flip-flop.
- Human comments: draft fix and reply for the user; post only after their yes. Answer every comment on its own thread.
- No ping before 4–5 days of silence, and then only a drafted, polite nudge for the user to post.
