# Self-grill

Run it **twice**: before writing code (questions 1–18) and again after the fix passes (all of them, 19–29 included).
Write the answers in the run log. Tag each **verified** (command, file:line, or data) or **assumed**. An assumed answer
that would change the fix is verified, or becomes one of at most 3 questions to the user, each with a recommended answer.

## The problem
1. What exactly does the user/reporter see that is wrong? Quote it.
2. Every expected result, numbered. Which are code, which are new UI/copy, which depend on a model or third party?
3. Which environments, versions, platforms, or input types does it cover? Which one was actually reported?
4. Which commit/version was running where it was seen?
5. Do comments say an earlier fix failed? What exactly failed?

## The evidence
6. Is there real data (ids, logs, DB records, a recording, a failing input)? What does it show? (`evidence-sources.md`: read-only, small queries, no personal data copied out)
7. Does the real data actually show the bug, or a different one?
8. One mechanism or several giving the same symptom? Which one did the reporter hit?

## Where it is and who else hits it
9. Which file:line on the deployed/default branch produces the symptom?
10. Every caller of the function you will change, on that branch.
11. An existing guard, helper, or library field that already solves part of it?
12. Other tickets, issues or call sites the same mechanism fully explains?

## Already done?
13. Any PR (any state), commit, or local branch for this? Is its content really on the deployed branch?
14. Is the current behaviour documented (docstring, comment, test, docs)? If yes, it is a design question, not a bug.

## Blast radius
15. What else reads the data or state you change (reports, other services, caches, exports, clients)?
16. Does anything users see change: a screen, message, wait, order, default, or output format?
17. Is anything a behaviour change: timing, retry, ordering, what gets written, public API?
18. Does it touch a public contract (API, CLI flags, config keys, file formats) that other projects depend on?

## Proof (after the fix)
19. Which input reproduces the bug on base, and what does the fixed code return for it?
20. For every write/side effect on the path: what happens if it runs twice (retry, resubmit, duplicate event)?
21. Edge cases covered: empty, null/None, zero, negative, very large, duplicate, out of order, concurrent, slow or failed network, cancellation, non-ASCII and right-to-left text, other OS, oldest supported version.
22. Which mutation of the fix makes a test fail? Did you run it?
23. Does each assertion of the new test fail on base on its own?
24. Which library versions does the build install, and does what you rely on exist in the lowest allowed version?
25. Lint/format/type warnings: same count as base or fewer?
26. Can any added line be deleted with all tests and expected results still passing? (shrink pass)
27. Is every claim in the explanation and PR/ticket text backed by a command output from this run?
28. What would the strictest reviewer of this repo ask first, and what is the one-line answer?

## Classification
29. Deterministic, model-dependent, needs repro, product decision, or already fixed — and why?
