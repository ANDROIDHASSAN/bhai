# Route: task (`/bhai <anything>`)

Goal: do exactly what was asked, nothing more, and prove it works.

1. **Restate** the task as a precise operation with a done-when. Two tasks in one → do both, in a stated order.
   Vague verb ("dekh lo", "fix it") → name the concrete operation. Question only → answer it; don't change code.
2. **Scope**: name the files/dirs in play and what is off-limits. Risky actions (delete, dependency, schema, push,
   deploy, revert) → ask first.
3. **Do it** with the spine: understand → reproduce or baseline → smallest change → prove → review.
4. **Explain** (`explain.md`). If something could not be verified, say so plainly instead of claiming it.
