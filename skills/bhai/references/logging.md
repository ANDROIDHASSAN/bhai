# Run log

Every run writes one Markdown file **outside the repo**, so it can never end up in a commit or PR:

`~/.bhai/runs/<YYYY-MM-DD>-<route>-<slug>.md`

Create the directory if missing. Write the file with the editor tool, not a shell redirect. Sections, filled as you go:

```
# <route>: <one-line restatement>
- input: <what the user typed>
- repo / branch / base commit: <...>
- done-when: <...>

## Decisions
- <time> <what was decided and why, one line each; rejected candidates with the reason>

## Commands and evidence
- `<command>` → <exit code, key output lines; failing-before and passing-after both quoted>

## Diff
<git diff --stat>

## Gates
<each gate: pass / fail / not applicable, with the evidence line>

## Outcome
<the explanation block shown to the user; what is pending on the user>
```

Never write secrets, tokens, `.env` values or personal data into the log. Never delete old logs; the user owns them.
