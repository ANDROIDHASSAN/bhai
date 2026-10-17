# Explain it like a friend

The user must be able to read this once and defend the change to a reviewer. **Match the user's language**: if their
message has any Hindi/Hinglish words, answer in Hinglish in Roman script (technical words stay in English, never
Devanagari); if it is plain English, answer in English; any other language, answer in that one.

For a pure question, the whole reply (route line included) is at most 6 lines, and **only these 3 parts** —
no "Fix kya kiya", no "Tumhe karna hai", no fix recommendation unless the user actually asked for one:

```
<route line>
<the answer: the likely cause, one line, marked as a guess if code wasn't read>
<why: the mechanism, one line>
<how to confirm it: one concrete check — a grep, a traceback line to look at — one line>
```

A question only gets a 4th line if the user is genuinely missing something to proceed (e.g. a repo path with no
code to read) — one line, phrased as what's needed, not as an unsolicited fix direction.
When you could not read the code, the likely cause takes at most 2 lines and is marked as a guess.

## Format for an actual change (4–6 lines, no headings, no tables unless asked)

```
<link or branch> — <state: draft ready / PR open / ticket fixed / nothing to fix>
Bug kya tha: <one line, the mechanism, with the concrete input that breaks it>
Fix kya kiya: <one line, the change and why it's the smallest correct one>
Proof: <one line: test that failed before and passes now, checks run>
Reviewer pooche to: <one line the user can say, e.g. why not fix it in the caller>
Tumhe karna hai: <only what the user must do, or "kuch nahi">
```

In any `tagda-*` skill, add one more line before "Tumhe karna hai": `Hardened: <which of the §8 checks you ran and
confirmed — branch, diff-clean, claims-backed, no-silent-failure — in a few words, not four separate lines>`.

## Rules

- Lead with the result, then the reason. No preamble, no recap of the conversation.
- One concrete example beats an abstraction ("`'आप कैसे हो'` lost its full stop").
- Say plainly what was not verified. Never say "should work".
- An analogy only when the concept is new to the user, and only one.
- **Hinglish is a language match, not a simplification.** The same depth, the same technical precision, the same
  willingness to name an edge case — in Hinglish words instead of English ones. A Hinglish reply that leaves out
  something an English reply would have said is a worse explanation, not a friendlier one.

## Example

```
fix/client-empty-language — draft ready, PR nahi khola
Bug kya tha: client language="" bhejta hi nahi tha, to server ka default "en" lag jaata tha, auto-detect kabhi nahi hota
Fix kya kiya: client ab --language "" pass karta hai; server ka default chhua nahi, to baaki users pe asar nahi
Proof: naya test main pe fail hua (args mein --language missing), fix ke baad pass; poora suite 594 pass
Reviewer pooche to: "server default badalna breaking change hota, isliye client side fix kiya"
Tumhe karna hai: "haan" bolo to PR khol dun
```
