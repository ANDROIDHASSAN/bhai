# The best fix is the shortest correct one

A fix is done when it removes the root cause for **every** caller and **every** acceptance item, with the fewest
changed lines, and a test proves both. Short but wrong is a second bug; correct but long is a review that never ends.

## 1. Acceptance list first

Number every expected result from the ticket/issue/task. A fix that meets 2 of 3 is a partial fix, and the
explanation must say which one is missing. No expected result written down → derive one and state it as an assumption.

## 2. Is a change needed at all?

Check before writing code:
- already fixed on the branch that is actually deployed (or the default branch) → prove it with the reported input, say "already fixed", no diff;
- an open PR or an unpushed local branch already exists for it → treat that code as an untested candidate, test it, don't write a parallel fix;
- it is config, data, or a product decision, not code → say so and stop.

## 3. Classify, and only `deterministic` proceeds without asking

| class | meaning | action |
|---|---|---|
| deterministic | the wrong output is decided by code you can change | fix |
| model-dependent | the outcome depends on an LLM/STT/TTS/third-party quality | stop, explain, no push |
| needs repro | the mechanism is not proven from code and real data | stop, ask for data |
| product decision | the expected result adds UI, copy, timing, or changes stored data | ask the user |
| already fixed | proven on the reported input | report, ask for a recheck |

## 4. Root cause, where every caller routes through

Trace the real flow from the user action to what is written or shown. Grep every caller of the function you will
touch; fix it once in the shared place. Then look for **siblings**: other tickets or call sites the same mechanism
explains. A sibling joins only if the same change also meets *its* expected result; otherwise list it as "related,
not fixed by this".

## 5. Climb the ladder, stop at the first rung that holds

1. Nothing to change (config/data/already fixed).
2. An existing helper, guard, or field in this codebase — fix the existing guard instead of adding a new one.
3. Standard library or platform feature.
4. An already-installed dependency.
5. One line.
6. The minimum new code that works.

No new dependency, schema change, renamed public path/queue/env value, or reformatting of untouched lines without the user's yes.

## 6. Prove it like a skeptic

1. **Base reproduces**: the same test/harness on the unfixed code shows the reported failure. A test that passes on base proves nothing.
2. **Cases**: one per acceptance item, the normal path (must behave exactly as before), and the edges that apply: empty, null, duplicate, retry, out of order, very long, non-ASCII/another language, slow or failed network, concurrent calls.
3. **Mutation check**: break the fix one way (remove the guard, flip the comparison); a case must fail.
4. **Parity**: lint/format/type error counts on base vs fixed, same tool both times; no new warnings.
5. **Dependency truth**: if the fix relies on a library default or field, read that library's source at the installed version (and the lowest version the range allows).
6. **Writes run twice**: for every write, counter or side effect on the path, ask what a retry, a duplicate event or a re-submit does. `+=`, append and read-then-set are not idempotent.
7. **Fakes follow the real rules**: a mock must keep the real event order and return values, or the test checks the mock.
8. A surprising result → suspect the check first.
