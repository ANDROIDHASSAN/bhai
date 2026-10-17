---
name: tagda-explain
description: "bhai's hardened explain-only mode: answers a question about a codebase with no code change, every claim checked against the actual code or a command run in this session instead of inferred or guessed — not capped at bhai's usual 5-10 line pure-question reply when the question genuinely needs more. Use when the user types /tagda-explain, says 'tagda explain', 'tagda samjha de', or wants a thorough, verified explanation of how something works or why a bug happens, without wanting it fixed."
---

# tagda-explain

bhai's plain-question path (`../bhai/SKILL.md`'s "question that needs no change" branch), run strict: the usual
5-10 line cap is lifted when the question genuinely needs more, but nothing in the answer is allowed to be a guess
presented as fact.

## How to run it

1. Read the actual code the question is about — every file and every caller involved, not just the one function
   named. Read `../bhai/skills/bhai/references/self-grill.md` questions 1-18 as a checklist for what "actually
   understood it" covers, applied as fast as a question needs, not the full repro-and-fix spine.
2. Hardened gate: **every claim traces to the code you read or a command you ran in this session.** "It's probably
   X" without having read the relevant code doesn't go in the answer — read the code first, or mark it as an
   explicit, labelled guess and say exactly what would confirm it (which file, which command).
3. If confirming the answer needs running something (reproducing a bug, checking a version, measuring something),
   run it before answering rather than describing what running it would probably show.
4. Write the answer in `../bhai/skills/bhai/references/explain.md`'s voice (plain, the user's language, one
   concrete example beats an abstraction) — but let it run as long as the question needs: a one-line bug has a
   one-line answer, a "why does this whole subsystem work this way" question gets the paragraphs it needs. Length
   is driven by the question, never by filling space.
5. No code is written, no branch created, nothing committed — if the user then wants it fixed, that's a separate
   `/bhai`, `tagda-fix`, or `tagda-commit` run.

## When not to reach for this

The user wants it fixed, not just explained → `/bhai` or `tagda-fix` (same question, but it ends in a diff).
