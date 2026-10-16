<h1 align="center">bhai</h1>

<p align="center"><strong>Give it a repo, a ticket, or a sentence. It reproduces the bug first, makes the smallest fix,<br>proves it, and explains it so you can defend it to any reviewer.</strong></p>

<p align="center"><em>Bhai, bas bol de.</em></p>

<!-- HERO: 15-second GIF — `/bhai <repo link>` → failing test → fix → green → Hinglish explanation. Record before launch. -->

> **Status: pre-release (v0.1).** The workflow is the one behind 16 merged pull requests in LiveKit, RealtimeSTT,
> Piper and Mastra in October 2026. Packaged as `/bhai`, it is being tested before the first public release.

## One command, three jobs

```text
/bhai https://github.com/owner/repo        → finds a real bug, fixes it, drafts a merge-worthy PR
/bhai ABC-123   (or a Jira/Linear/GitHub issue link)  → solves the ticket end to end
/bhai add retry with backoff to the uploader          → just does it, properly
```

Every route follows the same spine: **understand → reproduce → smallest fix → prove → review → gate → explain → log**.

## Why it doesn't break things

| It always | It never (without your yes) |
|---|---|
| reproduces the bug with a failing test first | pushes, opens a PR, comments, merges or deploys |
| runs the repo's own lint, type and test commands | force-pushes, adds a dependency, or edits lockfiles/versions |
| reverts the fix to check the test really catches it | claims a number it didn't measure |
| follows each repo's AI-contribution policy | opens more than 2 PRs in one repo |
| keeps the diff to the fix and its test | adds itself to your commits or PRs |

## The best fix is the shortest correct one

Before writing code it checks whether a change is needed at all (already fixed, config, data, a product decision),
fixes the root cause where every caller routes through, and reuses what the codebase already has before adding
anything. Then it proves the fix like a skeptic: the bug reproduces on the old code, one case per expected result,
and a mutation check that breaks the fix to make sure the tests notice. [Details](skills/bhai/references/fix-quality.md).

## What it needs from you

A link or a sentence, your GitHub CLI logged in, and a "haan" before anything is pushed, posted or merged.
For tickets, tracker access or the pasted ticket. If you can't explain the change to a reviewer after reading its
summary, don't approve it. [Full list](skills/bhai/references/user-contract.md).

## It explains like a friend

```text
fix/client-empty-language — draft ready, PR nahi khola
Bug kya tha: client language="" bhejta hi nahi tha, to server ka default "en" lag jaata tha
Fix kya kiya: client ab --language "" pass karta hai; server ka default chhua nahi
Proof: naya test main pe fail hua, fix ke baad pass; poora suite 594 pass
Reviewer pooche to: "server default badalna breaking change hota, isliye client side fix kiya"
Tumhe karna hai: "haan" bolo to PR khol dun
```

Hinglish by default; it answers in whatever language you write in.

## Install

```bash
# Claude Code
claude plugin marketplace add ANDROIDHASSAN/bhai
claude plugin install bhai@bhai
```

Other agents that read the Agent Skills format can load `skills/bhai/SKILL.md` directly.
<!-- Verify each agent before listing it here. -->

## Works better with

`bhai` uses these if you have them installed, and falls back to its own checklist if you don't:
a code-review command, a simplicity reviewer, and review-handling skills. See
[`skills/bhai/references/review.md`](skills/bhai/references/review.md).

## Every run is logged

One Markdown file per run in `~/.bhai/runs/`: the decisions, every command with its output, the diff, and each gate.
Outside your repo, so it can never land in a commit.

## License

MIT
