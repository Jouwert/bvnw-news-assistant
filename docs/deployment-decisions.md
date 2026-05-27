# Deployment decisions

This repository documents the deployment and runtime choices behind the BVNW news assistant.

## Keep the BVNW assistant separate from the main runtime
The BVNW workflow is implemented as a separate OpenClaw assistant/runtime path instead of being mixed into the main operator assistant.

That separation keeps the editorial scope narrow and reduces the chance that unrelated chat history or tooling bleeds into the neighbourhood-news flow.

## Use a private Telegram workflow instead of autonomous posting
The operator interface is a private Telegram workflow for shortlist delivery, selections, drafts, and follow-up.

In practice this included a dedicated BVNW editorial chat/channel for the assistant rather than a shared general-purpose operator chat.

That keeps human approval in the middle of the process.
The system is meant to support editorial work, not to publish neighbourhood updates on its own.

## Put a bounded webhook receiver in front of assistant handling
Inbound Telegram updates are received through a project-specific webhook receiver.

That receiver exists to:
- accept bounded updates;
- queue them durably;
- keep raw ingress separate from assistant execution;
- forward structured work items into the handling path.

This is a safer operational split than treating every inbound chat message as direct assistant context.

## Use queue and ledger files as the operational state backbone
The runtime uses queue/ledger handling instead of relying only on chat memory.

That allows:
- recoverable work-item tracking;
- per-item status inspection;
- response logging;
- documentation linkage for substantive runs.

For this workflow, inspectable state matters more than conversational smoothness.

## Make documentation part of the runtime contract
Substantive editorial work is written to dated run files.

That choice turns shortlist and drafting work into something that can be inspected later instead of disappearing into chat scrollback.

It also keeps the system useful even when the project is still in a private-pilot validation phase.

## Match model capability to editorial quality needs
The BVNW flow is bounded, but that does not automatically make it a good fit for weak models.

In actual project use, GPT-4o was tried for this workflow and did not work well enough for consistent shortlist and draft quality. The practical decision was to use more capable models when needed for the editorial step, even if smaller models remained attractive for cost-sensitive supporting work.

That reflects the task shape:
- narrow scope, but still quality-sensitive;
- repetitive editorial structure with room for subtle mistakes;
- approval-first operation, where bad drafts still waste operator time;
- day-to-day use, where reliability matters more than the cheapest possible default.

## Keep the output format strict
The final post format is intentionally constrained: one complete WhatsApp-ready post per fenced block, with source credit and simple copy/paste handling.

That is a deployment decision as much as a writing rule. It reduces downstream friction for the human editor.

## Treat source-photo retrieval as part of the workflow, not a bonus
The runtime guidance expects a source photo to be retrieved and sent when a usable public image exists.

That makes the workflow more complete for real editorial use, while still keeping the assistant bounded to approved source material.