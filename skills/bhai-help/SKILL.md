---
name: bhai-help
description: "Quick-reference card for everything bhai can do — the routes, the sibling skills, and how to invoke each. One-shot display, not a persistent mode. Use when the user asks 'bhai me kya kya hai', 'bhai help', '/bhai-help', 'what can bhai do', or 'how do I use bhai'."
---

# bhai-help

Print this card (adapt the wording, keep the content and structure) and stop — no tool calls, no route taken,
nothing fixed:

```
bhai — one command for real engineering work. Every route: understand → branch → reproduce → smallest fix →
prove → review itself → gate (your yes) → explain → log.

  /bhai <repo link>              find a real bug there, draft a merge-worthy PR
  /bhai <ticket link or key>     solve it end to end (Jira, Linear, GitHub issue)
  /bhai <anything else>         build it from scratch, same careful way
  /bhai status · /bhai watch <repo>   health check on every open PR/issue
  /bhai <a plain question>      no code change — just the answer, 5-10 lines

Sibling skills (same spine, different scope or pass):
  /tagda-fix <...>      everything /bhai does, with the failure-mode checklist
                         (branch-first, clean diff, proof-backed claims, no
                         silent failures) as a mandatory gate, not a self-check
  /tagda-build <idea>   tagda-fix, narrowed to building a real thing from a
                         rough idea — scoped spec, the laziness ladder, each
                         piece proven before the next
  /tagda-commit <repo>  tagda-fix, narrowed to open-source contribution only,
                         ends at a clean local commit ready for your yes
  /tagda-explain <...>  explain-only, no code change, every claim checked
                         against the actual code — not capped at 5-10 lines
                         when the question genuinely needs more
  /bhai-status          the status/follow-up route alone, no repo name needed
  /bhai-audit <repo>    scans for real, unclaimed bugs and reports them —
                         finds candidates, fixes nothing, opens nothing
  /bhai-help            this card

Hard rules, always: never pushes, opens a PR, comments, or merges without your
explicit yes in this session; never touches the default branch; your identity
only on every commit, no assistant co-author or footer.
```

If the user asks about one specific route or rule in more depth, answer that from `../bhai/SKILL.md` and its
`references/*.md` rather than re-printing the whole card.
