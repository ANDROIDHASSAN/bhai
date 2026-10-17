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
- Added `tagdafix` as its own skill (`/tagdafix`): the same routing as `/bhai`, with that hardened checklist made a mandatory gate instead of a self-check, reported in the route line and explanation.
