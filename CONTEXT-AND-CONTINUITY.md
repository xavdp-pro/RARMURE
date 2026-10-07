# Context and Continuity

## Why an existing conceptual framework can help

An established framework provides shared vocabulary and distinctions: intention, responsibility, authority, evidence, implementation, runtime behavior, and human acceptance. This can reduce repeated clarification and help collaborators interpret a new proposal at the intended level of abstraction.

The SHAPER separation between governance, operational substrate, and workspace is useful for locating responsibilities in RARMURE. It helps discuss a living memory without confusing its interface, storage, and decision rules.

This is an interpretation of the role of context, not a measured acceleration claim. There has been no controlled comparison between development with prior context and a cold start. Similar ideas could emerge without that history; the route, vocabulary, and clarification effort might differ.

## Memory, original material, and current evidence

A memory summary can support continuity but is selective and may become outdated. Access to original material is not equivalent to having reread it. Current source documents should be checked when an architectural claim depends on their exact content.

The initial formalization has been extended through a focused, detailed study of SHAPER OS V1.15 and SHAPER Three Layers. [SHAPER foundations](SHAPER-FOUNDATIONS.md) records the design contributions and versioned source map; [Scope and coverage](SCOPE-AND-COVERAGE.md) records the reading limits. This is not an exhaustive audit of either corpus.

Project documents state the adopted concept directly. Private source discussions and retrieval metadata are not project dependencies or public provenance.

## Avoiding inherited blind spots

Shared context can also anchor contributors to familiar concepts. Counter-review should ask whether a simpler explanation or architecture would satisfy the current need, whether inherited terminology hides ambiguity, and whether an earlier decision still applies.

Continuity should improve understanding while keeping assumptions revisable. Familiarity alone establishes neither correctness nor novelty.

## Context prepared for a role

A worker should receive the exact local state, relevant requirements and known interactions. A reviewer may need consumers and failure cases outside that local view. The master needs project-wide summaries and access to supporting evidence within its mandate. None of these roles automatically needs every historical record.

Prepared context should distinguish source facts, interpretation, proposal, adopted decision, and observation. It should identify versions, unresolved questions, data boundaries, and missing or stale information. When a session is lost or changed, reconstruct this context and reconcile unfinished operations before resuming effects.

## Lessons with conditions

A retained lesson records its supporting observations, applicability conditions, counterexamples, adoption status, and reason for review. For example, a failed authorization cache is evidence about that design under particular revocation conditions, not a universal prohibition on caching.

Keep observations stable while interpretations evolve. A later successful design may narrow an earlier lesson without erasing the original failure. This allows accumulated experience to guide exploration while preserving the ability to discover a better solution.
