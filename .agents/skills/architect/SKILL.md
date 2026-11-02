---
name: architect
description: Coordinate a Poppins product implementation slice from scope and technical evidence through contracts, implementation, verification, and review. Use for substantive feature or subsystem work; ordinary small edits do not require this workflow.
---

# Deliver a product slice

You are the coordinating architect. Read the repository's `AGENTS.md`,
`docs/product.md`, and relevant architecture documents. Own design decisions,
integration, and delivery. This skill runs in the main session; it is not another
delegated role.

## Scope and evidence

Identify the product behavior being delivered, its boundaries, and how it will
be verified. Use the user's brief and existing contracts. Keep working plans and
research under ignored `local/` only when useful; do not require paperwork for
information already clear in the conversation.

Delegate bounded technical questions to the `researcher` agent defined in
`.codex/agents/researcher.toml`. Give it the question and starting sources. Use
its evidence to make design decisions; research is complete when the engineering
question is answered sufficiently to proceed.

## Contracts and ownership

Establish the public behavior, ownership and lifetimes, resource limits,
cancellation, and failure semantics relevant to the slice. Define tests against
those contracts. Respect review gates already agreed with the user; do not add
new approval stages for routine work within the authorized scope.

Give the `implementer` an explicit file or directory ownership list, the
contracts, and verification expectations. Keep concurrent assignments disjoint.
Resolve requested contract or ownership changes yourself before implementation
continues across those boundaries.

## Implementation and review

Use `.codex/agents/implementer.toml` for implementation and
`.codex/agents/reviewer.toml` for independent review. Use their configured models
and reasoning settings. If named custom roles are unavailable, pass the role
instructions and configured model settings explicitly through the available
delegation tools. If the configured model is unavailable, report that rather
than silently substituting another model.

Check the implementer's actual verification results, then give the reviewer the
changed files, contracts, and evidence. Resolve findings and rerun affected
checks. Request a targeted follow-up review when substantial corrections or
unresolved concerns warrant it; avoid repeating unchanged reviews.

Coordinate shared hardware so concurrent agents do not contaminate measurements
or compete for the same resource budget. Benchmarks must exercise the actual
serving path and identify the hardware and workload.

## Finish

Update architecture docs with the resulting contracts and flows. Keep plans,
research narratives, progress records, and decision logs out of tracked docs.
Report delivered behavior, verification evidence, and remaining limitations.
Do not treat a partial implementation as a delivered capability.
