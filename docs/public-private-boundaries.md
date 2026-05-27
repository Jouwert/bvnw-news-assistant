# Public / private boundaries

This repository is a public documentation layer for the BVNW news assistant.
It describes the workflow shape, runtime design, and bounded editorial handling without exposing private operational content.

## Public in this repository
These are appropriate for public documentation:
- the high-level workflow from source sweep to final draft;
- the separation between Telegram ingress, queue/ledger handling, and editorial review;
- deployment choices such as private-group operation and bounded webhook design;
- sanitized examples of shortlist and final-post structure;
- minimal configuration snippets with placeholders instead of live values.

## Keep private
These should stay out of the public repo:
- raw Telegram messages and private group history;
- exact group IDs, routing identifiers, or chat targets;
- secrets, bot tokens, and secret-file contents;
- raw queue, ledger, replies, and wake logs;
- internal moderation notes or unpublished editorial debate;
- local machine paths and environment-specific secret locations;
- direct production endpoints that would make the runtime easier to probe.

## Sanitization rules used here
Public artifacts should:
- preserve the real workflow shape;
- preserve the relationship between webhook, queue, ledger, replies, and run files;
- use placeholders for ports, paths, URLs, and secrets when those are not the point of the artifact;
- replace private run content with synthetic or trimmed examples.

## Why this boundary matters
The project is useful precisely because it combines:
- private editorial handling;
- bounded assistant behaviour;
- durable state and documentation.

Publishing the workflow logic is useful.
Publishing the live private runtime content would weaken the same system the documentation is trying to explain.

## What the public layer is not
This repository is not:
- a dump of live Telegram interactions;
- a mirror of runtime state files;
- a claim that the workflow is already fully rolled out publicly;
- a promise of autonomous posting.

The public layer documents a private-pilot, approval-first editorial assistant.