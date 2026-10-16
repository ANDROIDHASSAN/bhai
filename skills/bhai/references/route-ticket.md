# Route: ticket (`/bhai <ticket>`)

Goal: the ticket closes with the smallest diff at the root cause, proven where the ticket was observed.

## 1. Read the ticket fully

- Jira/Linear: use the connected MCP or CLI if present; otherwise ask the user to paste the description. Read comments,
  attachments, linked tickets and the environment it was seen in.
- GitHub issue: `gh issue view <n> -R <r> --comments`.

Pin, one line each: **symptom** (technical words, not "it's broken"), **where observed** (URL/host/environment → which
repo and branch), **done-when** (one binary check).

Number every **expected result** bullet; that is the acceptance list. Read comments newest first: a "verified, not
fixed" comment means an earlier fix was wrong or never shipped — find out why. Pull any ids, URLs or logs from the
text and screenshots, and fetch the real data they point to when you have access: logs (Grafana/Loki and the like)
around the reported time and the exact database record, read-only, following `evidence-sources.md`. Real data beats theory.

## 2. Grill before code

Answer each question in the run log from code, logs or data you looked at, marked **verified** (with the command or
file:line) or **assumed**. Every assumed answer that would change the fix is verified or becomes one of at most 3
questions to the user, each with your recommended answer.
- Which repo owns this? If repo A only shows what B returns, the ticket belongs to B — follow the data, not the title.
- Which branch is actually deployed where it was seen? Reproduce against that remote branch, not a stale local tip.
- Is it already fixed on that branch, or is it config/data, not code? Then say so: no diff.
- **Siblings**: search the tracker and the code for other tickets/call sites with the same root cause. Fix the shared
  cause once and list every ticket it closes.

- Is it already fixed or in flight? Search merged and open PRs for the ticket key, check that a "merged" PR's content
  is really on the deployed branch, and look for unpushed local branches from earlier attempts.
- Classify it (`fix-quality.md` §3). Only `deterministic` continues without asking.

## 3. Fix and prove

Spine steps 3–6 with `fix-quality.md`. A dirty working tree is never touched without asking: use a new worktree cut
from the deployed branch. If the same fix must land on several long-lived branches, write it once and port it hunk
by hunk, diffing each hunk afterwards. Non-trivial logic leaves one runnable check behind.

## 4. Ship gate, then close the loop

- Run `gates.md` before any push/PR.
- Report: root cause (one line), tickets closed, diff size, blast radius, verification output, what was skipped and why.
- Draft the ticket comment for the user; post only on their yes.
