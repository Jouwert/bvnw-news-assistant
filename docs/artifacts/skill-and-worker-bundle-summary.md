# Skill and worker bundle summary

The later BVNW runtime kept the original MVP flow, but wrapped it in a more explicit worker/workspace bundle.

That bundle made the editorial assistant easier to run as a bounded subsystem instead of a loose general chat workflow.

## What the bundle adds
The later workspace materials show a small but important runtime structure around the assistant:
- dedicated agent identity files;
- narrower worker-facing instructions;
- a project-specific runtime folder for the BVNW webhook path;
- wake/queue handling that keeps editorial jobs separate from unrelated assistant work.

## Why this matters
The original project already had the core MVP shape: source sweep, Telegram review, drafting, and durable run files.

The later worker/workspace layer did not replace that MVP. It made the same workflow more operationally explicit:
- the assistant is treated as its own bounded editorial agent;
- queue items can wake the worker against a narrower task contract;
- runtime instructions live closer to the project instead of being implied from a broader operator environment.

## Relationship to the skill layer
The project also used a dedicated BVNW/OpenClaw skill layer to keep the editorial contract stable.

That skill-level guidance matters because this is not a generic chatbot task. The workflow expects:
- shortlist-first handling;
- neighbourhood relevance filtering;
- strict final-post formatting;
- source preservation and source-photo follow-up where available;
- human approval before publication.

## Public boundary
This summary documents the existence and role of the worker/workspace and skill layer.
It does not publish live runtime identifiers, secrets, internal group targets, or raw queue state.