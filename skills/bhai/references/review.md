# Self-review, like a senior developer who reviews their own diff before anyone else sees it

**Default: do this yourself, inline, in this same turn — no separate skill call.** A dedicated review skill
(`/code-review`, `/ponytail:ponytail-review`, ...) loads its own instructions into context on top of what's already
here, which costs real tokens for a check this checklist already covers at no extra cost. Reserve an actual skill
call for when the user explicitly asks for that specific tool, or for a pass this checklist genuinely can't do
(`/ponytail:ponytail-audit`'s whole-repo scan, only worth it on `tagda-build`'s bigger builds). Same rigor either
way — the checklist below isn't a lesser version, it's the same senior-developer review written out instead of
invoked:

- Does the new test fail on the default branch, **each assertion on its own**?
- Is every caller of the changed function still correct? Any other call site with the same bug?
- Smallest diff? No drive-by edits, renames, reformatting, or new files that could be avoided — `fix-quality.md`
  §5–6 (the ladder, the shrink pass) is this same question, asked twice on purpose.
- Does it read like it already belonged in this file? (`merge-readiness.md` §1's style-matching, done before
  writing — if it wasn't, that's a sign to go back and match the file's own idiom, not to add a separate pass now.)
- Error paths: anything swallowed, any early return that hides a failure, any resource left open?
- Does the diff match the explanation exactly? Any claim in the PR/ticket text not backed by a command output?

Report the review itself the way `/caveman` would — terse, no padding, whether or not that skill is actually
called: findings as short bullets, not a narrated walkthrough of how you checked.

Act on findings exactly as `/superpowers:receiving-code-review` would, whether or not it's installed: real and in
scope → fix with a test in a new commit. Real but out of scope → list under "Not changed". Wrong → note the
evidence; don't change code to please a reviewer, and don't flip-flop on a trade-off you already made for a reason.
