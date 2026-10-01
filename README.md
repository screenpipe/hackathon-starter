<!-- screenpipe — AI that knows everything you've seen, said, or heard -->
<!-- https://screenpipe.com -->
# Build agents that remember how work gets done

Watch someone do a real task, document it accurately, and help someone else repeat it. Three connected starters for the [42 Paris hackathon, October 16 to 18](https://luma.com/bnre6nou).

## Start with a workflow review

Install [Bun](https://bun.sh/docs/installation) 1.3 or newer:

```sh
git clone https://github.com/screenpipe/hackathon-starter.git
cd hackathon-starter
bun run demo
bun start
```

Open **http://localhost:4242**. No dependencies to install, Screenpipe account or AI key needed for the fictional sample. Review a paid-order reporting procedure, including a refunded order and a one-off browser problem that should not become a standard step.

![The workflow review desk](docs/dashboard.png)

## Three projects to fork

| Starter | Working example | Build further |
|---|---|---|
| [Work session → SOP](examples/work-session-sop/README.md) | Bring observed records into an unclassified draft, or explicitly ask your own AI provider to propose a procedure with exact source quotes. | Group repeated sessions, find missing context, compare normal work with exceptions |
| [Workflow review desk](examples/workflow-review/README.md) | Correct instructions, classify observations, answer questions, review evidence, export a frozen snapshot and start a separate revision. | Reviewer collaboration, screenshot provenance, process-owner sign-off |
| [Reviewed workflow → replay](examples/workflow-replay/README.md) | Check an approved snapshot, explicitly select a fixed reporting adapter, and test it on fresh input and an invalid case. | Add one carefully scoped integration and a measurable acceptance test |

The bundled candidate is curated fictional data, not proof that AI discovered a workflow. For your own captured work, the optional AI path actually takes observed records as input. It is unapproved output until a person checks it. We have tested the provider adapter with mocked responses; real-provider quality is unverified.

The review fingerprint detects changes to an exported artifact. Reviewer names are self-attested. This is a hackathon prototype, not authenticated enterprise approval, access control or an audit service.

## Try the full handoff

1. In the review desk, compare every instruction with its evidence. Keep the browser refresh classified as **troubleshooting**, not a normal process step.
2. Answer the open question. For the fictional sample, confirm that pending and refunded rows are excluded.
3. Check each reviewed observation, enter your name, then **Approve and freeze**. Export the approved JSON to a private location such as `local-data/approved.json`.
4. Read the [adapter contract](examples/workflow-replay/README.md). If it matches your reviewed procedure, run:

```sh
bun run replay --approved local-data/approved.json --orders sample-data/orders.csv --adapter paid-order-report-v1
bun run replay --approved local-data/approved.json --orders sample-data/orders-second.csv --adapter paid-order-report-v1
```

The first result contains `Atlas,150.00` and `Beacon,80.00`. The second contains `Atlas,10.30` and `Cedar,45.00`. Each run writes a new report and receipt under ignored `output/`, naming the procedure fingerprint, revision and reviewer.

```sh
bun run replay --approved local-data/approved.json --orders sample-data/orders-invalid.csv --adapter paid-order-report-v1
```

The invalid case must reject a duplicate order ID before writing a report. Replay runs fixed code, not AI-generated instructions. Choosing the adapter explicitly is your confirmation that its documented behavior fits the procedure; the prototype cannot verify that semantic match.

Start a new revision in the desk. Its checks reset, and the earlier exported approval remains unchanged. Have a teammate run the instructions without your help and record what they needed clarified.

## Connect your own work

Follow [local-data setup](docs/local-data.md). Capture a small, permissioned work session, inspect it, then:

```sh
bun run sop --input local-data/records.json
bun start --draft output/procedure-draft.json
```

This starts with unclassified observations and unknown context. To ask a configured AI provider for a proposed SOP instead:

```sh
bun run sop --input local-data/records.json --ai
```

Only `--ai` sends the selected records to that provider, which may charge separately. Unknown evidence IDs and non-matching quotes are rejected, but matching quotes do not establish that an instruction is correct or that the process is complete. The reviewer must make that judgment. No emails, CRM writes or browser actions are executed.

## Choose a useful problem

Use fictional or permissioned data for invoice investigation, order exceptions, onboarding handoffs, support escalation or another repeated task. [Project ideas and acceptance tests](ideas.md).

The event tracks remain **Agents That Remember**, **Your Data, Your Interface**, and **Wildcard**. These starters give the tracks a concrete starting point. They do not change the organizer's rules or judging criteria.

Optional smaller examples are still available: [meeting follow-up](examples/meeting-followup/README.md) and the [work-memory browser](examples/work-dashboard/README.md) at `/memory`.

## Participant resources

- [Event registration and organizer Discord details](https://luma.com/bnre6nou). Follow the organizer's `#hackathon-access` instructions.
- Participant Business access: the 30-day page is being prepared. Organizers will share it after activation is verified. The samples already work without a subscription.
- [Install Screenpipe](https://screenpipe.com/download), [local API setup](docs/local-data.md), [submission checklist](docs/submission.md).
- [Screenpipe MCP](https://github.com/screenpipe/screenpipe/tree/main/packages/screenpipe-mcp#installation), [cloud plugin](https://github.com/screenpipe/screenpipe-cloud), [Gemini CLI extension](https://github.com/screenpipe/gemini-cli-extension), [community projects](https://github.com/screenpipe/awesome-screenpipe).
- [Optional advanced River training project](https://github.com/screenpipe/river-ai-screenpipe-training), with separate compute/model requirements.

Run `bun test` and `bun run demo` to check your fork. Tests run on Mac, Windows and Linux. They cover grounding, review gates, unchanged snapshots, revision lineage, replay on two inputs and failure handling. CI is not evidence of production deployment or independent customer acceptance.

`local-data/`, `output/` and `.env` are ignored by Git. Exports contain quoted evidence, so inspect them before sharing. Capture and optional cloud services have their own [data flows](https://docs.screenpipe.com). Original sample code and fictional fixtures use MIT; Screenpipe and linked projects retain their own licenses.
