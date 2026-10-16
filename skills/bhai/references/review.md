# Self-review

Use the strongest reviewer that is installed, in this order, and run only one of each kind:

| If installed | Use it for |
|---|---|
| a code-review skill or command (e.g. `/code-review`) | correctness and regressions on the diff |
| a simplicity reviewer (e.g. ponytail review/audit) | over-engineering, needless code |
| a review-handling skill (e.g. superpowers receiving/requesting code review) | how to act on findings |

None installed → do it inline with this checklist:

- Does the new test fail on the default branch, **each assertion on its own**?
- Is every caller of the changed function still correct? Any other call site with the same bug?
- Smallest diff? No drive-by edits, renames, reformatting, or new files that could be avoided?
- Error paths: anything swallowed, any early return that hides a failure, any resource left open?
- Does the diff match the explanation exactly? Any claim in the PR/ticket text not backed by a command output?

Act on findings: real and in scope → fix with a test in a new commit. Real but out of scope → list under "Not changed".
Wrong → note the evidence; don't change code to please a reviewer, and don't flip-flop on a trade-off.
