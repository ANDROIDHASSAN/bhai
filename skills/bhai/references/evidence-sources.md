# Real data: logs and databases

Real data beats theory. When the user has these connected (MCP servers or CLIs), use them to see what actually
happened before deciding on a fix. Never set them up yourself and never ask for credentials in chat.

## What to look for

| Source | Use it for |
|---|---|
| Logs (Grafana/Loki, Datadog, CloudWatch, Sentry, `kubectl logs`) | the error and the 5 minutes around the reported time; the request/room/user id from the ticket; how often it happens (count over 7 days) and since which deploy |
| Metrics/traces | latency or error-rate change at a deploy; which service in the chain failed |
| Databases (Mongo, Postgres, MySQL…) | the one record the ticket is about; its state vs what the code expects; how many records are in the same bad state |

Find the time, environment and ids in the ticket first (text, URLs, screenshots). Match the environment: production
logs for a production ticket; a snapshot or replica only if the user says it is current enough, and say its date.

## Hard rules

- **Read-only.** Queries that read: find, count, aggregate, select, explain. Never a write, update, delete, DDL,
  `$out`/`$merge`, or a query on a connection the user marked as writable unless they explicitly ask.
- **Small and indexed.** Always a filter, only the fields you need, and a limit (≤ 50 rows/docs; logs: a narrow time
  window). Shared live servers get no unbounded scans; `explain` first when unsure an index exists.
- **Personal data stays where it is.** Names, emails, phones, transcripts, recordings, tokens: never in the PR, the
  ticket comment, the commit, the explanation or the run log. Quote ids, counts and aggregates instead.
- **Credentials never print.** Show config shape with values redacted.
- No access, or the source is down → say so and continue from code, marking those self-grill answers **assumed**.

## In the self-grill

Question 6–8 are answered from these sources when available: the real record or log line, the count of affected
rows/events, and whether the data shows this bug or a different one.
