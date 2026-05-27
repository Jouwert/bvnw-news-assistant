# Editorial output contract

The BVNW workflow is built around a strict editorial contract rather than free-form assistant conversation.

## Workflow shape
The core flow is:
1. source sweep;
2. shortlist delivery;
3. admin selection;
4. draft generation;
5. final post delivery;
6. source-photo retrieval attempt when a usable image exists;
7. durable run documentation.

## Shortlist behaviour
Shortlist messages are expected to preserve direct source links and enough context for a human editor to decide whether an item is worth drafting.

## Final-post behaviour
Final posts are designed for easy WhatsApp copy/paste.

The current rule is simple:
- one complete final post per fenced block;
- no splitting the same post across prose and fragments;
- source credit stays attached to the post.

## Documentation behaviour
Substantive editorial work is expected to leave a written trail in dated run files.

That makes the workflow inspectable and prevents editorial decisions from disappearing into chat history.

## Source-photo behaviour
When a usable source image is publicly available, the assistant is expected to try to retrieve and send it rather than giving up after a single failed attempt.

That rule matters because the workflow is meant for actual editorial use, not just text generation demos.