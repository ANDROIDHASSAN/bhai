# Route: contribute (`/bhai <repo link>`)

Goal: one merge-worthy PR the maintainers would have wanted, or an honest "nothing worth sending" report.

## 1. Measure the repo before touching code

Do `merge-readiness.md` §1 in full; the short version is below.

```bash
gh repo view <r> --json defaultBranchRef,isArchived,stargazerCount
gh pr list -R <r> --state merged --limit 60 --json number,title,author,additions,deletions,files,mergedAt,createdAt,mergedBy
```
Record in the run log: title style (conventional `fix(scope):` or plain sentence), median size, share touching tests,
changelog/fragment convention, sign-off (DCO), who merges, median hours to merge, **share of merged PRs from outsiders**.

Stop and report (no PR) if any of these hold:
- archived, or no outsider PR merged in the last 60
- CONTRIBUTING or AGENTS.md forbids AI-generated contributions, or requires an issue/assignment first that does not exist
- a CLA the user has not signed (tell the user; they sign it themselves)
- the user already has 2 open PRs in this repo

## 2. Find a real bug (in this order)

1. Run the README quickstart and examples on this machine; try edge inputs (empty, huge, non-ASCII, odd encodings, cancellation, missing optional deps).
2. Open issues with a reproduction, no linked PR, no assignee, no "I'll take this" comment.
3. Code reading **only as a lead**: it becomes a candidate after a runnable reproduction shows a user-visible wrong result.

A cheap, strong way to find bugs: a property probe. Feed many inputs (several languages, emoji, numbers, URLs,
abbreviations, empty) through the public API under every documented option, chunked whole, one character at a time and
randomly, and assert invariants: nothing lost or duplicated, same output however the input is chunked, docs match
behaviour. Then reproduce each violation with the smallest input.

Reject a candidate when the current behaviour is documented (docstring, comment, test), is a design question, or an
open PR already covers it. When README and docstrings disagree, that is a design question too: issue, not PR (`gh search prs --repo <r> "<keyword or #>" --state open`).

## 3. Fix and prove

Spine steps 3–6 from `SKILL.md` with `fix-quality.md`, using the repo's own commands. Aim for the repo's own median
PR size or smaller: one concern, the shared function not each caller, no drive-by edits. Each assertion of the new
test must fail on the default branch on its own. Compare failure lists before and after when the local
environment cannot run everything, and say so.

## 4. Draft, don't send

- Branch `fix/<short-name>` from the fresh default branch; one commit per logical change, in the repo's title style.
- Write the PR body in the repo's measured style: problem with a reproduction, the fix, tests run (quoted), scope.
- Run `merge-readiness.md` §2–3 (local CI, fresh merge of the default branch, re-search for duplicates).
- Show the user the explanation (`explain.md`) and the PR draft. Open it only after their yes — or, in `--auto` mode,
  open it without stopping when every gate passed (`user-contract.md`).
- After opening: read every bot review in full; fix real findings in new commits with a test and reply on that thread;
  never answer a human reviewer without the user's approval; never ping maintainers.
