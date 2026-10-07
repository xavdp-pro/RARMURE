# SHAPER foundations for RARMURE

RARMURE can apply SHAPER's way of connecting intention, bounded action, observation, and correction to collaborative code construction. The useful unit becomes a **code proposal connected to its purpose, assumptions, competing proposals, and evidence**. The code tree is one containment view of that richer graph.

This is a design synthesis for the concept stage. The mappings below extend the RARMURE proposal; they do not establish an implementation or adopt a SHAPER deployment profile. The [source map](#source-map) distinguishes the consulted SHAPER responsibilities from their proposed application here.

## Three responsibilities for one evolving program

SHAPER OS supplies design inspiration, not a mandatory runtime dependency. RARMURE may operate independently, using its own implementation of the authority, revision, review, and evidence contracts stated in this project. No SHAPER installation, service connection, or deployment profile is required. A future integration or formal corpus adoption would be a separate explicit choice; this conceptual mapping establishes neither integration nor compliance.

The SHAPER OS, Runtime, and Workspace distinction separates meaning, execution, and human interaction. It is different from both architectural perimeters and the RAM, database, and retrieval representations. [S1, S2]

| Responsibility | RARMURE application | Example |
| --- | --- | --- |
| OS | Purpose, mandates, invariant requirements, trade-off policy, evidence and revision rules | Define which correctness guarantees a speed-oriented variant must preserve |
| Runtime | Exact objects, revisions, causal events, permissions, experiments, durable state and recovery | Materialize two candidates and bind their results to exact source states |
| Workspace | Human and agent views of intentions, alternatives, disagreements and evidence | Show a growing code tree with a comparison view and a usable stop control |

RAM, persistence, and semantic retrieval belong primarily to the Runtime responsibility. A tree animation belongs to the Workspace. The master participates in applying decision policy; it is neither the storage authority nor the source of the human mandate.

This separation lets an interface, model, database, or source language change while the purpose and acceptance contract remain understandable.

## Preserve a graph beneath the tree

SHAPER distinguishes logical containment, authority, functional dependency, data ownership, and physical hosting. Those relationships must not be collapsed into one hierarchy. Its object space treats folders as representations of objects with identities and typed relations. [S1, S2]

RARMURE should therefore distinguish at least three structures:

- A containment view: project, folders, files, functions and other elements.
- A dependency graph: calls, shared state, interfaces, requirements, tests and evidence.
- An exploration graph: alternatives, derivations, combinations, objections and decisions.

The same function can appear in several explorations without duplicating its identity. Two candidates can form a composition; a requirement can cross several directories. An agent's presence on a parent folder does not confer ownership or authority over every child.

The semantic reference resolves an exact object in a chosen view. Similarity helps discover related objects; it does not decide that two objects are identical. Likewise, a declared intention describes expected effects, while a dependency edge describes an observed or inferred relationship. Both can be incomplete.

## Make cooperation a feedback loop

SHAPER distinguishes a signal, an observed gap, its interpretation, an action, and the resulting effect. It also treats unexpectedly good outcomes as useful signals. [S2, S3]

For RARMURE, the recurring loop becomes:

**Intention → candidate → observation → discrepancy or useful surprise → competing explanations → counter-review → discriminating experiment → decision → qualified lesson.**

Suppose a combined test slows down after two agents modify related code. That is an observation. “The new security check caused the regression” is a hypothesis. Another explanation could be a changed fixture or a cache interaction. The discussion should produce an experiment that separates these explanations, rather than immediately undoing the security change.

An unusually fast candidate deserves the same attention: is the gain reproducible, did it skip required work, and under which conditions can it be reused? Learning only from failures would miss useful discoveries.

Every observation needs a named observer and limits. A compiler, benchmark, dependency extractor, agent reviewer, and human user see different parts of the result. A green test indicator cannot certify all of them.

## Let disagreement improve the next experiment

Counter-review should reveal different assumptions, missing observations, and alternative explanations. SHAPER separates this function from decision authority and allows the correction mechanism itself to be questioned. [S2, S3, S5]

A discussion attached to a code object should retain:

| Record | What it preserves |
| --- | --- |
| Claim | The proposed behavior and its applicable conditions |
| Objection | A specific counterexample, missing condition, or challenged assumption |
| Discriminating check | What observation would help resolve the disagreement |
| Result | The exact tested state and the observed outcome |
| Disposition | Revise, combine, retain separately, defer, reject, or select within scope |

A minority objection can be decisive even when every other agent agrees. Conversely, an objection may itself rely on a mistaken requirement or outdated state. Provider identity is useful context, but independence should be assessed through differences in evidence, assumptions, tools, and approach.

Reviews also need feedback. Did they find a real interaction? Did they block valid work? Did their advice introduce a regression? Repeated objections with no new evidence should trigger a change of method or a scoped stop. Review is proportionate; it should not create an infinite approval chain.

## Give each role the context its judgment requires

SHAPER separates reasoning depth, throughput, and context horizon. Its cognition bridge distinguishes a logical session from a provider session and from durable operations. Its consulted-context design separates designing the framework, acting within a task, and supervising the result. [S4]

RARMURE can use four context horizons without making them a ranking of agent intelligence:

| Horizon | Typical content |
| --- | --- |
| Immediate input | Exact target, requested transformation and relevant local contract |
| Current session | Current intentions, candidates, discussions and recent observations |
| System context | Callers, dependencies, permissions, global requirements and accepted state |
| Accumulated use | Prior decisions, operating evidence, human priorities and qualified lessons |

A local worker may need a narrow working set. A reviewer of a shared interface needs its consumers. The master needs summaries across the project, with access to supporting evidence inside its mandate. Broad context should be available through deliberate retrieval and escalation, not copied indiscriminately into every request.

A prepared context should identify its sources and revisions, missing or stale information, current mandate, selected requirements, affected relationships, unresolved objections, and expected evidence. It should expand when a dependency or decision requires it. A declared horizon is not proof that the information was actually supplied.

Shared history can reduce repeated clarification and preserve the reason behind a requirement. It can also anchor agents to old choices. Its benefit remains a hypothesis to evaluate against a cold start, with comparable tasks and budgets.

## Keep memory informative and revisable

SHAPER's epistemic distinctions and learning loop support separating recorded observations from their interpretation and from adopted rules. [S3, S5]

RARMURE should preserve four distinguishable kinds of memory:

1. Exact source states and experimental observations, with provenance.
2. Interpretations and hypotheses, including disagreements.
3. Decisions and mandates, with the scope and authority that made them applicable.
4. Lessons, with applicability conditions, counterexamples and reasons to revisit them.

For example, “cache proposal A failed after permission revocation under conditions C” is useful evidence. “Caching must never be used” is a generalization requiring further justification. A later proposal that caches only permission-independent work should be assessed against the actual failure conditions.

Changing a lesson must preserve its connection to the original observation. Replacing an interpretation must not rewrite historical test results. Retention and deletion rules still apply to each data class; preserving meaning does not require retaining every transient message forever.

The semantic index is a derived route into these records. Entries identify represented revisions and their status. If embeddings are unavailable, that absence must be visible; exact or lexical retrieval can remain available without being mislabeled semantic retrieval.

## Make the master accountable at both scales

SHAPER aligns knowledge, responsibility, and control while keeping intelligence separate from authority. Its fractal pattern repeats the relationship between intention, boundary, action, evidence and correction, without requiring an identical implementation at every scale. [S1, S2, S5]

For RARMURE, local coordinators should return bounded conclusions: what works, under which assumptions, what remains unresolved, and what other scopes they affect. The master then examines compatibility and project acceptance. A local improvement can reveal a better global approach; a global requirement can invalidate a locally attractive candidate.

The master should select within declared priorities, preserve alternatives, and expose the evidence behind its choices. It may ask for a discriminating experiment rather than another opinion. It must not silently weaken the specification to make a preferred candidate pass. Requirement revisions are separate decisions made under the relevant authority.

The same control pattern can repeat at function, module, service, and project scale. The amount of review, context, and testing varies with impact. Recursion depth, active exploration paths, spending, elapsed time, and no-progress conditions need explicit bounds. Stabilization, sleep, resumption, and retirement are valid states of a living system.

## Separate working views from assessed candidates

SHAPER's conversational test workspace distinguishes a draft from its baseline and from the exact snapshot tested. Runtime event handling also distinguishes requested, accepted, executed, and verified effects. [S2, S6]

RARMURE should distinguish the following states and views:

| View | Meaning |
| --- | --- |
| Working view | Mutable provisional changes derived from a known base, with associated intentions and hypotheses |
| Candidate | A fixed proposed state; an experiment additionally needs a suitable manifest and execution context |
| Assessed candidate | A fixed candidate with assessment records; checks may pass, fail, or remain inconclusive |
| Selected composition | The options chosen for combined validation |
| Accepted candidate | A fixed state accepted by an authorized role against a stated specification and scope |

An accepted realization may remain usable while new exploration paths develop. New exploration cannot silently alter what an earlier acceptance meant. The canonical present is directly accessible only to the master among agents. Workers receive issued candidate views, and any supported file-tool edit returns to a view-specific virtual change buffer as a proposal against its base. Pinned test inputs remain unchanged; see [present authority and virtual exploration](ARCHITECTURE.md#present-authority-and-virtual-exploration).

A completed tool call or journal receipt is insufficient proof of the intended software behavior. Timeouts can leave effects uncertain. On resumption, inspect the operation record and actual state before retrying. A provider session is not the action ledger, and restarting an agent does not erase its unresolved obligations.

## Keep the human view useful

The Workspace responsibility is to make the authorized situation understandable and controllable. [S2]

The tree should help answer ordinary questions: What are the agents trying? What changed? Where do they disagree? Which variant is ready to compare? What is the reason for this choice? What would make us reconsider it?

An overview can show active areas, competing variants, blocking interactions and evidence freshness. Selecting a node reveals its source, requirements, discussions, tests and decisions. Unknown, stale, untested and rejected states should remain distinct. Information should be routed to affected participants rather than broadcast to everyone.

Stopping work, revoking a mandate, inspecting the accepted source and exporting a fixed state should remain possible when a model provider is unavailable. These controls belong to the runtime and interface contract; they cannot depend solely on an agent deciding to cooperate.

## Bound the transfer into RARMURE

The strongest transferable pattern is **stable responsibilities with revisable implementations and interpretations**. RARMURE's current documents retain that pattern while leaving its technology choices open.

The consulted sources also contain particular infrastructure profiles, product roles and historical naming. They do not automatically choose RARMURE's database, container technology, interface framework, provider, or deployment topology. A later decision to adopt a SHAPER profile would require an explicit applicability map. [S1, S7]

The fractal and breathing metaphors express recursive exploration and stabilization. They provide no mathematical convergence guarantee. A logical intermediate representation and latent communication remain separate, deferred research. The explicit object and evidence protocol is sufficient to describe the initial concept.

## A bounded experiment to make the idea testable

A future experiment could reuse the authorization-and-cache example in [Requirements and validation](REQUIREMENTS-AND-VALIDATION.md). Two workers propose changes to one behavior. A reviewer challenges their interaction. The master compares compliant alternatives under performance and security profiles.

The experiment should demonstrate that exact identity survives a rename, overlapping intentions remain visible without ownership locks, an objection leads to a useful test, stale evidence is detected, and resumption does not duplicate an accepted operation. It should also record whether review wrongly blocks a valid alternative.

Measure time to a correctly accepted change, missed interactions, unnecessary blocking, coordination cost, and recovery behavior against a simpler baseline. A later comparison can isolate the effects of shared history, semantic retrieval, and model diversity. This would test which parts help, rather than crediting every gain to the whole concept.

## Source map

Reading date: 2026-10-07. SHAPER OS V1.15 was inspected at revision `a50d4d112049577543ed13762c3f483fbe498def`; SHAPER Three Layers at `a8eddf95b30a5952267990928e65c5e9c61131f8`. These references identify source responsibilities; the RARMURE applications above are design inferences.

| Reference | Consulted foundation |
| --- | --- |
| S1 | SHAPER OS [Intent](https://github.com/xavdp-pro/SHAPER-OS-V1.15/blob/a50d4d112049577543ed13762c3f483fbe498def/INTENT.md), [Law](https://github.com/xavdp-pro/SHAPER-OS-V1.15/blob/a50d4d112049577543ed13762c3f483fbe498def/LAW.md), [Layers and scopes](https://github.com/xavdp-pro/SHAPER-OS-V1.15/blob/a50d4d112049577543ed13762c3f483fbe498def/docs/learning/02-LAYERS-AND-SCOPES.md) |
| S2 | Three Layers [OS](https://github.com/xavdp-pro/shaper-three-layers/blob/a8eddf95b30a5952267990928e65c5e9c61131f8/10-SHAPER-OS/00_MASTER.md), [Runtime](https://github.com/xavdp-pro/shaper-three-layers/blob/a8eddf95b30a5952267990928e65c5e9c61131f8/20-SHAPER-RUNTIME/00_MASTER.md), [Workspace](https://github.com/xavdp-pro/shaper-three-layers/blob/a8eddf95b30a5952267990928e65c5e9c61131f8/30-SHAPER-WORKSPACE/00_MASTER.md), [Object space and RAG](https://github.com/xavdp-pro/shaper-three-layers/blob/a8eddf95b30a5952267990928e65c5e9c61131f8/40-TRANSVERSAL/03_OBJECT_SPACE_RAG.md) |
| S3 | SHAPER OS [Metacognition](https://github.com/xavdp-pro/SHAPER-OS-V1.15/blob/a50d4d112049577543ed13762c3f483fbe498def/docs/human/METACOGNITION.md), [Cooperative ecology](https://github.com/xavdp-pro/SHAPER-OS-V1.15/blob/a50d4d112049577543ed13762c3f483fbe498def/docs/design/COOPERATIVE-ECOLOGY.md) |
| S4 | SHAPER OS [Cognition](https://github.com/xavdp-pro/SHAPER-OS-V1.15/blob/a50d4d112049577543ed13762c3f483fbe498def/docs/architecture/COGNITION.md), [Cognition bridge](https://github.com/xavdp-pro/SHAPER-OS-V1.15/blob/a50d4d112049577543ed13762c3f483fbe498def/docs/intents/cognition-bridge.md), [Consulted context](https://github.com/xavdp-pro/SHAPER-OS-V1.15/blob/a50d4d112049577543ed13762c3f483fbe498def/docs/design/CONSULTED-CONTEXT.md) |
| S5 | SHAPER OS [Rules](https://github.com/xavdp-pro/SHAPER-OS-V1.15/blob/a50d4d112049577543ed13762c3f483fbe498def/RULES.md), [Operating contract](https://github.com/xavdp-pro/SHAPER-OS-V1.15/blob/a50d4d112049577543ed13762c3f483fbe498def/docs/agent/OPERATING-CONTRACT.md), [Evidence and learning](https://github.com/xavdp-pro/SHAPER-OS-V1.15/blob/a50d4d112049577543ed13762c3f483fbe498def/docs/learning/06-EVIDENCE-RECOVERY-LEARNING.md) |
| S6 | Three Layers [Synchronization](https://github.com/xavdp-pro/shaper-three-layers/blob/a8eddf95b30a5952267990928e65c5e9c61131f8/40-TRANSVERSAL/05_PROTOCOL_SYNC_OFFLINE.md), [Conversational test workspace](https://github.com/xavdp-pro/shaper-three-layers/blob/a8eddf95b30a5952267990928e65c5e9c61131f8/40-TRANSVERSAL/14_CONVERSATIONAL_AGENT_TEST_WORKSPACE.md) |
| S7 | Three Layers [Agnostic method translation](https://github.com/xavdp-pro/shaper-three-layers/blob/a8eddf95b30a5952267990928e65c5e9c61131f8/00-META/07_AGNOSTIC_METHOD_TRANSLATION.md), SHAPER OS [Materialization](https://github.com/xavdp-pro/SHAPER-OS-V1.15/blob/a50d4d112049577543ed13762c3f483fbe498def/docs/learning/05-MATERIALIZATION.md) |

The [coverage record](SCOPE-AND-COVERAGE.md) states the scope and limits of this study. Implementation and future experiments remain governed by the [current mandate](AGENTS.md).
