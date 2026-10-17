# Gates (run before anything leaves the machine)

Answer each from tool output in this session. Any "no" → fix it or stop and tell the user.

1. **Reproduced**: the new test (or command) failed before the fix, for the stated reason.
2. **Green**: the repo's own lint, format, type and test commands passed on this exact commit; output quoted.
3. **Negative control**: with the fix reverted, the new test fails; fix restored.
4. **Only this change**: run `git diff <base> --stat` and paste it. It must show only the fix and its test (plus a changelog fragment/version bump only where the repo's own rules require it). A lockfile, a version file, reformatted lines you didn't need to touch, or a scratch/debug script you created while investigating — `git checkout --` or `rm` it, then re-run the stat, before moving on. Don't report done with an unexplained file in the diff.
5. **No secrets**: no keys, tokens, `.env` contents, internal hostnames or personal data in the diff, commit message or PR text.
6. **Identity**: commit author is the user; no assistant co-author trailer or generated-by footer.
7. **Claims are evidence**: every number and "fails on main" in the PR/ticket text came from a command run here.
8. **Policy and caps**: repo's AI policy followed; at most 2 open PRs from the user in this repo; CLA/DCO handled.
9. **User said yes** to this specific push/PR/comment, in this session — or `--auto` covers it (`user-contract.md`).
10a. **Merge-ready**: workflows run locally, default branch freshly merged with no conflicts, no duplicate PR/issue appeared (`merge-readiness.md`).
10. **Never**: force-push to a branch with an open PR, commit or push to the default branch, or merge on the user's behalf —
    not even when the user asks for it, and never offer it as an option. Offer a branch + PR instead.
