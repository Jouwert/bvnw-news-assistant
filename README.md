# bvnw-news-assistant

Documentation for an **OpenClaw-based** bounded neighbourhood-news drafting workflow for **Bewonersvereniging Wageningen Noordwest (BVNW)**.

## What is in scope
This repository brings together four related parts of the workflow:
- a **source sweep and shortlist layer** for local Noordwest / Binnenveld signals;
- a **private Telegram editorial interface** for shortlist review, selection, and drafting;
- a **bounded webhook and runtime layer** with queue/ledger handling;
- a **durable run archive** for inspectable editorial work and reusable output patterns.

## Background
This workflow is built to help BVNW publish short, useful neighbourhood micro-updates without turning the process into uncontrolled autoposting.

The practical goal is to surface relevant local items, let an editor choose what matters, and produce WhatsApp-ready draft posts with a clear editorial trail.

That means the workflow is built around:
- public-source collection;
- shortlist-first review;
- mandatory human approval;
- bounded Telegram handling;
- durable run documentation;
- recoverable runtime state.

## Components

### Source sweep and shortlist layer
The source side filters public local signals into a smaller candidate set.

Topics:
- local-signal collection;
- shortlist curation;
- neighbourhood relevance filtering;
- source-link preservation for review.

### Telegram editorial interface
Telegram is the operator-facing surface for shortlist delivery, selections, drafts, and follow-up.

In the real project this includes a dedicated private editorial channel for the BVNW assistant rather than a shared general assistant chat.

Topics:
- private editorial workflow;
- approval-first operation;
- shortlist-to-draft flow;
- final post delivery.

### Bounded runtime layer
The runtime separates inbound Telegram handling from assistant execution.

Topics:
- webhook reception;
- append-only queueing;
- ledger-based item tracking;
- direct reply sending;
- recoverable handling state.

### Run archive and output layer
Substantive editorial runs are documented to disk instead of living only in chat.

Topics:
- durable run files;
- shortlist and draft records;
- final post formatting rules;
- documentation linkage in runtime state.

## Repository scope
This repository focuses on:
- workflow structure;
- component boundaries;
- deployment decisions;
- the relationship between Telegram ingress, bounded runtime handling, and human editorial review.

It does not include private group content, raw runtime state, or secrets.

## Repository contents
```text
bvnw-news-assistant/
├── README.md
└── docs/
    ├── architecture-overview.md
    ├── candidates-sanitized-technical-artifacts.md
    ├── deployment-decisions.md
    ├── public-private-boundaries.md
    ├── sanitized-technical-artifacts.md
    └── artifacts/
        ├── editorial-output-contract.md
        ├── editorial-run-example.md
        ├── minimal-webhook-compose.yaml
        ├── queue-ledger-runtime-summary.md
        ├── skill-and-worker-bundle-summary.md
        └── webhook-receiver-summary.md
```

## Public / private boundary
This repository documents architecture and workflow logic.
It does not publish:
- raw Telegram chat content;
- private group identifiers or internal routing details;
- secrets, tokens, or secret-file contents;
- raw queue, ledger, or replies logs;
- unpublished source photos or internal moderation notes.

See [`docs/public-private-boundaries.md`](docs/public-private-boundaries.md).

## Current status
This repository documents the BVNW news assistant as a real MVP/pilot, review-first editorial workflow with a first set of sanitized technical artifacts derived from the real project materials.

The underlying project already produced multiple real shortlist, draft, and final-post files, and the private Telegram workflow was used for actual handling rather than only for planning.

## Impact
- The workflow makes it feasible to publish neighbourhood news regularly with very little time and budget.
- Instead of drafting every item from scratch, editors review a shortlist, select promising items, and work from bounded drafts. That greatly lowers the effort required to keep community communications active.
- Useful local signals from chats and submissions are less likely to get lost, because they are turned into a structured editorial queue.
- The result is a practical human-in-the-loop publishing flow that helps attract people into the neighbourhood WhatsApp community without requiring a full editorial team.

## Next likely additions
Likely next additions:
- one sanitized note on source-photo retrieval behaviour;
- one small artifact around deduplication/archive checks;
- one later cleanup pass that removes candidate-only notes once the repo settles.