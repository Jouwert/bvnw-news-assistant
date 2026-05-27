# Architecture overview

The BVNW news assistant is an OpenClaw-based bounded editorial workflow for neighbourhood micro-news.

It is built as a separate runtime with its own Telegram interface, queue/ledger state, and run archive rather than as an open-ended assistant chat.

## High-level shape
The workflow has four main layers:
1. public local sources;
2. a private Telegram editorial surface;
3. a bounded runtime for receiving and tracking work items;
4. durable run documentation for shortlist, draft, and final output history.

## Source layer
The workflow starts from public local signals that may matter to Wageningen Noordwest, the Binnenveld, or nearby access routes.

The source side is not meant to publish everything it finds. It narrows a wider public source stream into a shortlist that is small enough for editorial review.

## Telegram editorial layer
Telegram is the operator-facing surface for the workflow.

It is used for:
- shortlist delivery;
- editorial selection;
- draft review;
- final post delivery;
- follow-up around source photos when available.

This layer is intentionally private and approval-first. The workflow is designed for editorial handling inside a closed operator context, not for autonomous public posting.

The real project materials show both direct bot handling and a dedicated private editorial group/channel for the assistant, so the operator surface is narrower and more purpose-built than a normal chat assistant setup.

## Webhook and ingress layer
Inbound Telegram updates do not go straight into open-ended model context.

Instead, a project-specific webhook receiver:
- accepts bounded Telegram updates;
- appends them to queue storage;
- forwards structured work items into the assistant wake path;
- keeps the raw ingress step narrow and inspectable.

That split reduces drift and makes the assistant easier to reason about operationally.

## Runtime state layer
The bounded runtime keeps track of work through queue and ledger files instead of relying on chat memory alone.

The runtime layer records:
- inbound work items;
- per-item handling state;
- reply records;
- documentation linkage for substantive editorial runs.

This gives the workflow a recoverable trail even when the editorial interaction itself happens in Telegram.

## Run archive layer
Substantive work is documented to dated run files under the project archive.

Those files capture things like:
- shortlisted candidates;
- why items were or were not chosen;
- draft post text;
- final post format;
- sources used.

The archive is part of the working system, not an afterthought.

## Output contract
The runtime is shaped around a small, repeatable output pattern:
- shortlist first;
- explicit selection;
- one clean final post block for copy/paste;
- source credit;
- source-photo delivery attempt when a usable image exists.

## Operational posture
The architecture is deliberately narrower than a general-purpose assistant:
- private Telegram workflow instead of public posting;
- bounded ingress instead of raw chat injection;
- queue/ledger state instead of conversational memory alone;
- durable run files instead of undocumented editorial decisions.

That is the core design choice behind the project.

In later iterations, the same workflow was also given a more explicit worker/workspace bundle so the editorial agent could be woken against queue items with narrower runtime instructions.