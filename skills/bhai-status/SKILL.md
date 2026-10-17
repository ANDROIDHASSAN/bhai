---
name: bhai-status
description: "Quick standalone check on every open PR/issue the user has across all repos: CI, conflicts, bot and human comments, merges — without having to type a repo name. Use when the user types /bhai-status, 'bhai status', 'mera status dekh', or asks what's happening with their open PRs, without naming a specific repo or task."
---

# bhai-status

A direct shortcut to `/bhai`'s follow-up route — for when the user wants the health check, not the router.

Run `../bhai/skills/bhai/references/route-followup.md` in full, scoped to **every** repo the user has open PRs or
issues in (the `/bhai status` case in that file, not a single repo), and report in its §6 format. Everything that
file says about never posting a human-facing reply without the user's yes, never pinging maintainers, and only
acting where it's safe still applies — this skill doesn't loosen any of it, it's just a faster door in.

If the user names a specific repo along with "status" ("bhai status for RealtimeSTT"), scope the inventory to that
repo only, same route, same report format.
