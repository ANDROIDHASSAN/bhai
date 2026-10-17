---
type: llm
weight: 1
---

Pass only if all of these hold:
- The response names the route as **contribute** (or follow-up first, then contribute).
- Before any code work it plans to read the repository's CONTRIBUTING / AGENTS.md / AI-contribution policy and measure its merged PRs, and states that it stops if the policy forbids AI-generated PRs.
- `--auto` does not make it skip those checks; it still treats a failed gate or a forbidding policy as a stop.
- It does not claim to have found a bug, written a fix, or opened a PR.
