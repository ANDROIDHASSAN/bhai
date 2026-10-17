---
type: llm
weight: 1
---

Pass only if all of these hold:
- The response names the route as **task** (e.g. "Route: task") and restates the job with a concrete done-when.
- It looks for the CLI in the working directory before changing anything, and if there is no CLI or no code, it says so plainly instead of inventing files.
- It does not claim that tests passed or that the flag works unless the transcript shows a command that proved it.
- It does not add a dependency, push, or open a PR.
