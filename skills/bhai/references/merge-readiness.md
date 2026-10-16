# Merge-readiness: make the PR the easiest yes the maintainer has all week

No tool can guarantee a merge; the maintainer decides. What bhai guarantees is that nothing *on our side* blocks it:
no conflict, no red check, no style mismatch, no missing step from the repo's own process.

## 1. Learn how this repo merges (before the fix)

```bash
gh pr list -R <r> --state merged --limit 100 --json number,title,author,additions,deletions,files,mergedBy,mergedAt,createdAt,labels,body
gh api "repos/<r>/pulls?state=closed&per_page=100" --jq '.[] | select(.merged_at) | "\(.number) \(.author_association)"'   # author_association is only in the REST API
git log --format='%an|%s' -200 <default-branch>            # commit subject style of the people who commit
gh api repos/<r>/contents/.github/CODEOWNERS --jq .content | base64 -d   # who owns the files you touch (if present)
ls .github/PULL_REQUEST_TEMPLATE* .github/workflows/ CONTRIBUTING* AGENTS.md CLAUDE.md 2>/dev/null
```
Record in the run log:
- **outsider PRs** (`author_association` CONTRIBUTOR/FIRST_TIME_CONTRIBUTOR/NONE) that merged: their size, title, body
  length, whether they touched tests, how many commits, how long they waited. **Copy that shape**, not the maintainers'.
- who merges which paths (and CODEOWNERS for the files you touch);
- required pieces: PR template sections, changelog fragment, DCO sign-off, CLA bot, issue-first rule, labels;
- the maintainers' own words in CONTRIBUTING, the PR template, and recent review comments on outsider PRs
  (`gh api repos/<r>/pulls/<n>/comments` on 5–10 of them): what they asked contributors to change is what to do upfront.
- with web access: the project's contributing guide on its docs site and maintainer posts about contributions.

## 2. Run CI before CI runs

Read every workflow in `.github/workflows/` that triggers on `pull_request`. Run the same commands locally (same tool
versions where the workflow pins them): lint, format, type check, tests, docs build, license/header checks.
A step you cannot run locally (secrets, GPU, OS) → say so in the run log and in the PR body's test section.

## 3. Right before opening

```bash
git fetch upstream && git merge upstream/<default-branch>   # no conflicts; rerun the checks if anything came in
git diff upstream/<default-branch> --stat                   # only the fix, its test, and required fragments
```
Re-search open PRs and issues for the same bug (someone may have opened one while you worked). Found → don't open.

## 4. After opening

Watch the first CI run and the bots (`route-followup.md`). A red check caused by our diff is fixed in a new commit
within the same run. If the repo needs a maintainer to approve CI for first-time contributors, say so; don't push
extra commits to trigger it.

## What still can't be controlled

A maintainer's priorities, a design disagreement, the project being quiet, or a competing PR merged first.
bhai reports these honestly instead of promising a merge.
