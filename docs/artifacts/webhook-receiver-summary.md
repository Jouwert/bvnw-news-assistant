# Webhook receiver summary

The BVNW workflow uses a narrow webhook receiver in front of the editorial runtime.

## Role in the system
The receiver exists to do a small number of things well:
- accept inbound Telegram updates;
- validate the request path or tokening scheme;
- append the update to queue storage;
- forward a structured wake payload into the assistant handling path.

That keeps the ingress step inspectable and bounded.

## Request handling pattern
The real project files show two webhook entry patterns:
- a protected endpoint used for manual testing;
- a Telegram-compatible path-secret endpoint for live webhook delivery.

In both cases, the receiver turns the inbound update into a queue entry instead of treating it as direct assistant context.

## Queue-first behaviour
The receiver writes inbound updates to append-only queue storage before the rest of the runtime acts on them.

That gives the system a durable intake trail and avoids coupling Telegram delivery directly to drafting behaviour.

## Wake forwarding
After queueing a live Telegram webhook update, the receiver sends a structured payload into the assistant wake path.

That payload carries only the fields needed to start handling work, such as:
- source;
- chat identifier;
- update identifier;
- text when present;
- the original update object.

## Why this matters
This split provides a cleaner operational boundary:
- Telegram ingress remains narrow;
- work can be inspected after the fact;
- assistant handling can fail or retry without losing the inbound event;
- the workflow stays closer to a small message-processing system than to an open-ended chat bot.

## Public note
The public repo keeps the receiver shape and behaviour, but not the live secrets, exact endpoint values, or local runtime paths used by the private system.