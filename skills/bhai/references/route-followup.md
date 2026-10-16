# Route: follow-up (`/bhai <repo>` when the user already has PRs there, `/bhai status`, `/bhai watch <repo>`)

Goal: keep every open PR/issue of the user healthy, act only where it is safe, and report in a few lines.
This runs **before** contribute: an existing PR that needs attention always beats a new one.

## 1. Inventory

```bash
gh pr list -R <r> --author @me --state all --limit 30 --json number,state,title,mergeable,updatedAt,reviewDecision
gh search prs --author @me --state open --limit 100      # /bhai status: every repo
gh search issues --author @me --state open --limit 100
```
Compare with the previous run log for this repo (`~/.bhai/runs/*-followup-<repo>.md`): what changed since then?
Nothing changed → say so in one line and stop.

## 2. For each open PR

| Finding | Action |
|---|---|
| CI red because of our diff | fix in a **new commit** with a test, rerun the repo's checks, push (user already approved this PR) |
| CI red, not our diff | re-run once if allowed; still red → report, don't touch |
| conflict with the default branch | merge the default branch into the PR branch (no rebase, no force-push), resolve, rerun checks, push |
| bot review (Devin, CodeRabbit, Copilot, Sourcery…) right | fix with a test in a new commit, reply on that thread naming the commit |
| bot review wrong | reply on the thread with evidence (command output, file:line); don't change code to please it |
| **human** comment or review | **never post.** Prepare the fix on the branch locally without pushing, draft the reply, show both to the user |
| CLA/DCO request, close-without-merge, design question | report to the user; don't act |
| PR body claim made stale by a new commit | update the body in the same run |

## 3. On a merge

Sync the fork's default branch with upstream, delete the merged branch on the fork and locally, note it in the run
log, and celebrate it in the report.

## 4. Capacity, then new work

If the user has fewer than 2 open PRs in this repo after the steps above, continue with `route-contribute.md`
(one new PR at most per run). Otherwise report "at cap" and stop.

## 5. Watching

`/bhai watch <repo>` repeats this route on a schedule, only after the user says yes to the interval. Use the agent's
own scheduler if it has one (e.g. a loop or cron tool); otherwise tell the user to re-run `/bhai <repo>`.
Suggested: hourly for repos with open PRs, never more often than every 30 minutes. Never ping maintainers; a PR with
no human activity for 5+ days gets a drafted, polite nudge for the user to post, nothing automatic.

## 6. Report (short)

```
Status: <PR link> <merged/open/needs action> — one line each, grouped merged / needs action / waiting
Maine kya kiya: <fixes pushed, bot replies, syncs>
Tumhe karna hai: <human replies to approve, CLA, decisions — or "kuch nahi">
```
