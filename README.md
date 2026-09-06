# n8n-data

Data store for the n8n triage analytics pipeline
(source: [skomp/n8n-test](https://github.com/skomp/n8n-test)).

## Files

| File | Contents |
|---|---|
| `issues.ndjson` | One JSON object per line, one line per issue, keyed by `number`. Triaged issues of `n8n-io/n8n` — those carrying any of 33 `triage:*`, `team:*` or `closed:*` labels. |
| `state.json` | Sync watermark: the highest `updatedAt` seen. The incremental sync queries from `watermark - 5 minutes` and de-duplicates on upsert. |

## How it is produced

`issues.ndjson` was backfilled once, locally, with `npm run backfill` in the source
repository: 55 GraphQL pages, 385 of 5,000 hourly rate-limit points, ~3.5 minutes.
A scheduled n8n workflow then syncs incrementally — roughly 20 records a day.

Do not hand-edit these files. They are machine-written and the sync upserts by
issue number.
