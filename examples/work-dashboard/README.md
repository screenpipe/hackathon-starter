<!-- screenpipe — AI that knows everything you've seen, said, or heard -->
<!-- https://screenpipe.com -->
# Personal work dashboard

Run `bun start` and open http://localhost:4242. Six fictional records are loaded. Search for `Maya` to see two records, or choose `Spreadsheet` to see the reporting task. Clear the filters to restore all records.

The interface is in `web/`, and the loopback server is `src/server.ts`. It renders recorded text as text, not HTML. Source links accept only local Screenpipe frame/timeline forms.

To load real records, follow [local-data setup](../../docs/local-data.md), then run `bun start --input local-data/records.json`. The server reads that file once at startup. Restart it after a new capture.

Fork ideas: group by project, annotate a decision, build a study timeline, add a local embedding search, or create a debugging handoff. If you add sharing, keep it explicit and decide what leaves the user's machine.
