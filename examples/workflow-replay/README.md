<!-- screenpipe — AI that knows everything you've seen, said, or heard -->
<!-- https://screenpipe.com -->
# Work session to a repeatable report

Run `bun run workflow` and read `output/workflow.md`. It describes a fictional observed routine: filter an order export to paid rows, sum per customer and save a separate report.

Run `bun run workflow --approve` to execute that specific routine on `sample-data/orders.csv`. Expected output in `output/paid-orders.csv`:

```csv
customer,total
Atlas,150.00
Beacon,80.00
```

Change the sample input or use `--orders path/to/orders.csv`. Duplicate IDs, invalid amounts and unexpected statuses cause refusal before a report is written. Only simple, unquoted CSV is supported. The replay writes inside `output/` and makes no network calls.

This is a bounded replay example. The procedure is supplied as reviewed sample steps; it is not a general model that discovers and automates arbitrary computer work. To extend it, use Screenpipe to retrieve a repeated work session, draft the procedure, review it, then add a narrowly defined operation with its own validation. Keep model output separate from executable shell commands.
