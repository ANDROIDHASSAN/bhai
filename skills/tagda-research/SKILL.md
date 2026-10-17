---
name: tagda-research
description: "bhai's hardened research mode: investigates a question that needs looking beyond this one codebase — comparing libraries or approaches, checking what a real repo's contribution policy says, sizing up whether an idea is feasible, finding prior art — and reports findings with sources, never a guess presented as fact. No code change. Different from `tagda-explain` (which answers from code already in front of you) and from bhai's own internal `research.md` (the research behind bhai's own rules, not a tool for the user's questions). Use when the user types /tagda-research, says 'tagda research kar', 'pata laga ke bata', or asks to compare options, check feasibility, or find out what's actually true about something outside the current file."
---

# tagda-research

For when the answer isn't sitting in the file you're already looking at — it needs a web search, reading a few
repos' own docs, or comparing more than one option. Same hardening as every `tagda-*` skill, aimed at the one
failure mode research is most prone to: a confident-sounding claim nobody actually checked.

## How to run it

1. **Scope the question first.** What's actually being decided or found out, and what would count as a good-enough
   answer — a yes/no, a ranked shortlist, a number with its source. A vague ask ("research X") → restate it as the
   specific question before doing anything.
2. **Go deep, not one search deep.** This is the one place bhai deliberately spends more effort than usual: don't
   stop at the first search result. Read the library's own docs/changelog, the repo's own CONTRIBUTING.md/issues,
   and — for anything technical enough to have one — the actual paper, RFC, or design doc behind it, the way
   `../bhai/skills/bhai/references/research.md` cites real arXiv/ACM papers instead of paraphrased secondhand
   claims about them. For a comparison or a "what does the evidence actually say" question, pull from several
   independent sources (papers, official blogs, real engineering write-ups, not just the first SEO result) and
   check whether they agree before concluding anything. When comparing options, check each one against the same
   criteria, not whichever facts were easiest to find for each. A topic that's genuinely broad or unsettled is
   worth a web search in extended/thorough mode, not the quick one.
3. **Hardened gate: every finding names where it came from.** A claim with no source — a doc, a file, a command's
   output, a search result — doesn't go in the report; mark it as an open question instead of filling the gap with
   a guess. If sources disagree, say so and which one is more current/authoritative, rather than picking one
   silently.
4. **Report** in `../bhai/skills/bhai/references/explain.md`'s voice: the answer first, then why, then the sources.
   Length follows the question — a one-line fact gets a one-line answer with its source; a real comparison gets a
   short table or list, not an essay padded to look thorough.
5. No code is written, no branch created, nothing committed — research informs a decision; it isn't the decision's
   implementation. If the user wants it acted on, that's a separate `/bhai`, `tagda-fix`, `tagda-build`, or
   `tagda-commit` run.

## When not to reach for this

The answer is already in the code you have open → `tagda-explain`. You want it built or fixed, not just
researched → `tagda-build`, `tagda-fix`, or `tagda-commit`.
