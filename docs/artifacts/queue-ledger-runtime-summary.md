# Queue and ledger runtime summary

The BVNW runtime uses queue and ledger files as its operational memory.

## Queue role
Inbound Telegram updates are appended to queue storage first.

The queue acts as the durable intake layer for new work items.
That means the system does not depend on ephemeral chat state alone.

## Ledger role
The ledger records handling state per inbound item.

In the real runtime files, ledger entries capture things like:
- an item identifier derived from chat/update information;
- received and handled timestamps;
- chat and update metadata;
- handling status;
- reply metadata when an acknowledgment or response is sent.

## Replies log role
A separate replies log keeps a lighter append-only record of outbound handling events.

That gives the system a second inspectable trail beyond the main ledger file.

## Documentation linkage
The project docs make documentation part of the runtime contract for substantive editorial work.

That means the state model is not just about whether a message was handled. It also carries linkage to dated run files and documentation status fields so the editorial trail remains inspectable.

## Why this design is useful
This structure supports:
- recoverable work handling;
- simple per-item inspection;
- separation between ingress and editorial action;
- durable linkage between Telegram handling and written run artifacts.

For a small review-first editorial assistant, this is more useful than relying on chat history as the only record of work.