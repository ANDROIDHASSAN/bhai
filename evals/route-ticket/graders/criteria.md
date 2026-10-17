---
type: llm
weight: 1
---

Pass only if all of these hold:
- The response names the route as **ticket**.
- It tries to read the whole ticket first, and since it cannot fetch it with the available tools, it asks the user for access or for the pasted ticket (description, expected results, comments, screenshots) instead of guessing what the ticket says.
- It does not invent a symptom, a root cause, or a fix for a ticket it has not read.
- It does not post any comment and does not claim to have changed code.
