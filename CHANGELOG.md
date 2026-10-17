# Unreleased

## Added

- Introduced the `bhai` command as a unified interface for repository work, ticket resolution, and general task execution.
- Established quality rules for fixes and defined a clear user contract.
- Implemented follow-up routes for status updates, watching repositories, and PR management.
- Added a code shrink pass and efficiency rules to the fix checklist.
- Incorporated merge-readiness checks and an `--auto` mode.
- Integrated self-grilling, PR crafting rules, and the research behind them.
- Enabled reading logs and databases for evidence-based decision-making, with read-only access.
- Completely rewrote the README with a new logo, demo, flow diagram, and FAQ.
- Updated the README with a chat hero, typing banner, animated dividers, and section emojis.
- Captured lessons from the first real run, a bug found in KoljaB/stream2sentence.
- Added Claude plugin evaluation cases and fixed issues identified by them.
- Introduced a guide for managing low credit situations.
- Hardened the contribute route against failure modes measured on free-tier backends: branch before the first edit (never commit on the default branch), a stricter "only this change" gate that catches stray lockfiles, reformatting and scratch files, and a rule against turning a loud bug into a silent one.
- Added the `tagda` family of hardened sibling skills, all starting with `tagda-` like `ponytail-*` does for ponytail: `tagda-fix` (any route, strict), `tagda-build` (building a real thing from a rough idea — scoped spec, the laziness ladder, each piece proven before the next), `tagda-commit` (open-source contribution only, strict, ends at a clean local commit; asks which repo or what kind if none is named instead of guessing), `tagda-explain` (explain-only, no code change, every claim checked against the code instead of guessed, not capped at bhai's usual 5-10 lines when the question needs more), and `tagda-research` (goes beyond the current codebase — papers, docs, real articles, more than one source compared — every finding sourced, no code change).
- Added three more single-purpose sibling skills: `bhai-status` (the follow-up route alone, no repo name needed), `bhai-audit` (scans one or more repos for real, unclaimed bugs and reports a ranked list — fixes nothing, opens nothing), and `bhai-help` (a quick-reference card for every route and sibling skill).
