# Route: contribute (`/bhai <repo link>`)

Goal: one merge-worthy PR the maintainers would have wanted, or an honest "nothing worth sending" report.

## 1. Measure the repo before touching code

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

Reject a candidate when the current behaviour is documented (docstring, comment, test), is a design question, or an
open PR already covers it (`gh search prs --repo <r> "<keyword or #>" --state open`).

## 3. Fix and prove

Spine steps 3–6 from `SKILL.md`, using the repo's own commands. Compare failure lists before and after when the local
environment cannot run everything, and say so.

## 4. Draft, don't send

- Branch `fix/<short-name>` from the fresh default branch; one commit per logical change, in the repo's title style.
- Write the PR body in the repo's measured style: problem with a reproduction, the fix, tests run (quoted), scope.
- Show the user the explanation (`explain.md`) and the PR draft. Open it only after their yes.
- After opening: read every bot review in full; fix real findings in new commits with a test and reply on that thread;
  never answer a human reviewer without the user's approval; never ping maintainers.
