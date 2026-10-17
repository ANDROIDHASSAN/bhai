---
# Low on Claude credits

bhai's workflow (gates, self-grill, the explain format) is model-agnostic. If you're close to a usage limit or
between billing cycles, you can keep working on a free-tier backend without losing any of it.

## 1. Check first

- `claude` prints remaining budget in its status line; `/cost` in-session gives a number.
- [ccusage](https://github.com/ryoppippi/ccusage) (community tool, not Anthropic's) reads your local session logs
  and shows burn rate and time-to-depletion across Claude Code and other CLIs.

## 2. Point Claude Code at a free-tier backend

Claude Code reads its API target from environment variables, so any OpenAI- or Anthropic-compatible gateway works:

```bash
export ANTHROPIC_BASE_URL="<your gateway's URL>"
export ANTHROPIC_AUTH_TOKEN="<its key>"
unset ANTHROPIC_API_KEY
claude
```

A few open-source gateways that proxy free-tier models this way (unaffiliated with bhai; read each one's README
and ToS before use): [OmniRoute](https://github.com/diegosouzapw/OmniRoute), a self-hosted router you run yourself
and configure with your own free-tier provider keys, or a local llama.cpp/Ollama server for a fully offline backend.
Pick one, or run several behind a router with automatic fallback.

## 3. The gates matter *more* here, not less

Free and smaller models follow instructions less reliably than Claude does. Don't loosen anything because the
backend changed:

- Keep using your coding agent's tool-permission allowlist (e.g. Claude Code's `--allowedTools`) to enforce the
  push/PR/comment gate **at the tool level**, not just by asking the model to behave — a weaker model may ignore a
  text rule but still can't call a tool it was never granted.
- Re-run the self-grill and the mutation check before trusting a free-model fix; they cost nothing and catch more
  on a weaker model, not less.
- If a free model's output looks wrong, say so and either retry on a different free model or finish the step on
  Claude. Don't relay a fix you haven't verified just because it came from a different backend.

## 4. Resuming where you left off

Every bhai run writes to `~/.bhai/runs/`. Point the next session (on any backend) at that file and it can continue
the same task from the same decisions and evidence, instead of starting over.
---
