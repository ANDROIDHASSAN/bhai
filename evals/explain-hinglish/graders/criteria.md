---
type: llm
weight: 1
---

Pass only if all of these hold:
- Apart from the first "Route: …" status line (which may be in English), the answer is in **Hinglish written in Roman script** (Hindi words in Latin letters), with technical terms (KeyError, token, hash, WebhookReceiver) kept in English. No Devanagari.
- It is short: at most about 8 non-empty lines in total, leading with the answer.
- It does not present a guess as a fact: anything not checked against code it actually read is marked as likely or unverified.
