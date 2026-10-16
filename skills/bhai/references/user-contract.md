# What bhai needs from the user

Tell the user this the first time they run `/bhai` in a session (short version, 3 lines), and again whenever one of
these blocks the run. Never work around a missing item; ask for it.

## Before a run

| Route | The user gives | Why |
|---|---|---|
| contribute | a repo link; their GitHub CLI logged in (`gh auth status`) | to read PRs/issues and, later, open a PR as them |
| ticket | a ticket link/key, plus tracker access (an MCP or CLI for Jira/Linear) **or** the pasted description and screenshots | bhai reads the whole ticket, comments and attachments |
| task | one sentence of what they want and, if not obvious, which repo/folder | to scope the change |
| all | a clean working tree, or permission to work in a new worktree/branch | bhai never touches uncommitted work |

## During a run

- Answer at most 3 questions, each asked with bhai's recommended answer (reply "haan" to accept).
- Provide anything only a human can: real data or a screenshot of the bug, a signed CLA, account access, product decisions.

## Before anything leaves the machine

- Read the explanation block. If it does not make sense to you, say so: bhai explains again or drops the change.
  **Don't approve a PR you can't defend to a reviewer.**
- Say "haan" (or "yes") to each push, PR, issue/ticket comment, or merge. Approval is per action, not per session.

## After

- Human reviewer comments: bhai drafts the fix and the reply; you approve before it posts.
- Merges, deploys and QA rechecks stay with you and your team.
