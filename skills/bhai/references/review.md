# Self-review, like a senior developer who reviews their own diff before anyone else sees it

Use the strongest reviewer installed for each concern — never more than one of a kind, and in this order, each
only once:

| Concern | Tool, if installed | Fallback (none installed) |
|---|---|---|
| Correctness, regressions on the diff | `/code-review` | the inline checklist below |
| Over-engineering, needless code, a diff that's bigger than it needs to be | `/ponytail:ponytail-review` | `fix-quality.md` §5–6 (the ladder, the shrink pass) |
| A whole-repo pass for leftover bloat (only on `tagda-build`'s bigger builds, not every small fix) | `/ponytail:ponytail-audit` | skip — not worth it for a small diff |
| Framing the ask before requesting review, so the reviewer sees a diff that already explains itself | `/superpowers:requesting-code-review` | `pr-craft.md`'s PR-body pattern |
| Acting on what a reviewer (bot or tool) comes back with — verify technically, don't just agree or flip-flop | `/superpowers:receiving-code-review` | the "act on findings" rule below, unchanged |
| How the review itself gets reported back (terse, no padding) | `/caveman` | `explain.md`'s own format is already terse; don't also pad it |

A senior developer's habit either way: the smallest diff that is still obviously correct, not the cleverest one —
`fix-quality.md`'s ladder and shrink pass exist for exactly this, whether or not `ponytail` is installed to check it.

None of the above installed → do it inline with this checklist:

- Does the new test fail on the default branch, **each assertion on its own**?
- Is every caller of the changed function still correct? Any other call site with the same bug?
- Smallest diff? No drive-by edits, renames, reformatting, or new files that could be avoided?
- Error paths: anything swallowed, any early return that hides a failure, any resource left open?
- Does the diff match the explanation exactly? Any claim in the PR/ticket text not backed by a command output?

Act on findings: real and in scope → fix with a test in a new commit. Real but out of scope → list under "Not changed".
Wrong → note the evidence; don't change code to please a reviewer, and don't flip-flop on a trade-off.
