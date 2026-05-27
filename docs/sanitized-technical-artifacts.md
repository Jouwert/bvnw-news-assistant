# Sanitized technical artifacts

This repository includes a first set of sanitized technical artifacts derived from the real BVNW project files.

## Implemented artifacts

### [`docs/artifacts/webhook-receiver-summary.md`](artifacts/webhook-receiver-summary.md)
Summary of the bounded Telegram webhook receiver: append-only queueing, secret-protected ingress, and asynchronous wake forwarding into the assistant runtime.

### [`docs/artifacts/queue-ledger-runtime-summary.md`](artifacts/queue-ledger-runtime-summary.md)
Summary of the runtime state model around queue items, ledger tracking, replies logging, and documentation linkage for substantive editorial work.

### [`docs/artifacts/editorial-output-contract.md`](artifacts/editorial-output-contract.md)
Short operational summary of the shortlist → selection → final-post contract, including the single-code-block output rule and the expectation to try source-photo retrieval when possible.

### [`docs/artifacts/editorial-run-example.md`](artifacts/editorial-run-example.md)
Sanitized example showing how shortlist notes and final post structure are represented in the project’s run artifacts.

### [`docs/artifacts/minimal-webhook-compose.yaml`](artifacts/minimal-webhook-compose.yaml)
Cleaned deployment snippet showing the minimal container shape for the webhook receiver without live paths, secrets, or production-specific routing details.

### [`docs/artifacts/skill-and-worker-bundle-summary.md`](artifacts/skill-and-worker-bundle-summary.md)
Short summary of the later BVNW worker/workspace bundle and the dedicated skill layer used to keep the editorial agent narrow, repeatable, and easier to wake from queue items.