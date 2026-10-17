---
name: tagda-build
description: "bhai's hardened build-from-an-idea mode. `/tagda-build <a rough idea>` turns it into a real, working thing — a project, a feature, a tool — with the smallest honest scope, tests that prove each piece, and the failure-mode checklist (branch before the first edit, diff/tree holds only what's needed, every claim backed by a command, no trading a loud bug for a silent one) as a mandatory gate, not a self-check. Use when the user types /tagda-build, says 'tagda bana de', 'idea se bana de', 'ekdam tagda banade', or wants something built from scratch properly and completely, not a small change to existing code — for a small task on an existing codebase, /bhai or tagda-fix fits better."
---

# tagda-build

The task route (`../bhai/skills/bhai/references/route-task.md`), run strict, for the specific case of building a
real thing from a rough idea — a project, a feature, a tool — not a small change to code that already exists.

## 1. Turn the idea into a spec

An idea is not a done-when. Before writing anything:
- Restate it as what the thing actually does, for whom, and the one or two things it must get right. Two ideas
  mashed together → split them, say which one this run builds.
- Name what's explicitly out of scope — the fastest way an "idea" run balloons is scope nobody asked for.
- Missing something a real build can't proceed without (which language/stack, where it runs, who uses it) → ask,
  max 3 questions. Everything else → pick the most ordinary, boring answer and say you picked it, don't ask.

## 2. Build with the ladder, not the first idea that comes to mind

`../bhai/skills/bhai/references/fix-quality.md` §5, applied to new code the same as a fix: nothing → an existing
helper or pattern already in this codebase → the standard library → a platform feature → an already-installed
dependency → one line → the minimum new code. A new dependency only when every rung above it genuinely doesn't
reach, and only for something load-bearing, not a convenience. Three similar lines beat a premature abstraction;
build the thing that's needed now, not the one that might be needed later.

## 3. Prove each piece as you build it, not at the end

A real build is several pieces, not one diff. For each piece: a test (or a runnable command whose output shows it
working) before moving to the next piece, same as `/bhai`'s reproduce-then-fix discipline — except there's no bug
to reproduce, so the "before" state is simply "doesn't exist yet, and the test says so." Wire the pieces together
only once each one is proven alone.

## 4. Review it like a peer would, before the hardened gates

Once it's built and proven piece by piece, step back and read the whole thing as a reviewer would, not just the
pieces as you wrote them: `../bhai/skills/bhai/references/self-grill.md` (all 29, answered from what you actually
ran) and `../bhai/skills/bhai/references/review.md`. Fix what's real and in scope now, before the hardened gates
below — a peer review that happens after the gates is a peer review that gets skipped under time pressure.

## 5. Hardened gates — mandatory, not a self-review pass

Checked before the final report, same four as every `tagda-*` skill:
- `git branch --show-current` is not `main`/`master`/`trunk` (existing repo) or the project has its own clean
  initial commit, not a pile of uncommitted scaffolding (new repo) — branch or init first, before the first file.
- `git diff <base> --stat` or `git status --short`, pasted, shows only what this build needed — no leftover
  scaffolding, debug script, or generated file that doesn't belong in the result.
- Every claim ("the tests pass", "it runs", "handles X") traces to a command actually run in this session.
- A fallback/except path added anywhere is checked for what it does to the caller — silently swallowing a real
  failure is not accepted in place of surfacing it.

If any of these would fail, **stop and say which one** rather than reporting it done.

## 6. Explain and stop before anything outward-facing

Route line: *"Route: task · mode: tagda build · symptom: X · done when: Y"*. `../bhai/skills/bhai/references/explain.md`'s
format, plus the `Hardened:` line. Push, a new repo going public, or anything else outward-facing still needs the
user's explicit yes in this session — building it is not the same as shipping it.

## When not to reach for this

A small, scoped change to code that already exists → `/bhai` or `tagda-fix`. Open-source contribution → `tagda-commit`.
A question, nothing to build → `tagda-explain`.
