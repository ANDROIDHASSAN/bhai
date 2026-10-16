# Route: ticket (`/bhai <ticket>`)

Goal: the ticket closes with the smallest diff at the root cause, proven where the ticket was observed.

## 1. Read the ticket fully

- Jira/Linear: use the connected MCP or CLI if present; otherwise ask the user to paste the description. Read comments,
  attachments, linked tickets and the environment it was seen in.
- GitHub issue: `gh issue view <n> -R <r> --comments`.

Pin, one line each: **symptom** (technical words, not "it's broken"), **where observed** (URL/host/environment → which
repo and branch), **done-when** (one binary check).

## 2. Grill before code

Ask yourself, and answer from evidence:
- Which repo owns this? If repo A only shows what B returns, the ticket belongs to B — follow the data, not the title.
- Which branch is actually deployed where it was seen? Reproduce against that remote branch, not a stale local tip.
- Is it already fixed on that branch, or is it config/data, not code? Then say so: no diff.
- **Siblings**: search the tracker and the code for other tickets/call sites with the same root cause. Fix the shared
  cause once and list every ticket it closes.

## 3. Fix and prove

Spine steps 3–6. A dirty working tree is never touched without asking. Work on a new branch from the deployed branch.
Non-trivial logic leaves one runnable check behind.

## 4. Ship gate, then close the loop

- Run `gates.md` before any push/PR.
- Report: root cause (one line), tickets closed, diff size, blast radius, verification output, what was skipped and why.
- Draft the ticket comment for the user; post only on their yes.
