# Scope and Coverage

Date: 2026-10-07. Delivery type: concept documentation and retained illustrations.

## Capability inventory

[Short explanation and detailed concept](PROJECT-EXPLANATION.md) provides a consolidated account and maps every C01–C41 idea to its explanation. The subject documents below remain canonical; the synthesis introduces no additional implementation claim.

| ID | Capability or idea | Canonical coverage | State |
| --- | --- | --- | --- |
| C01 | Shared human specification | [Requirements](REQUIREMENTS-AND-VALIDATION.md) | Documented |
| C02 | Living tree and mathematical breathing | [Vision](VISION.md) | Documented metaphor |
| C03 | Recursive parallel exploration and multiple viable paths | [Vision](VISION.md), [Cooperation](AGENT-COOPERATION.md) | Documented |
| C04 | Exact code, files, folders, functions, and documents in a graph | [Architecture](ARCHITECTURE.md) | Documented |
| C05 | Stable semantic references and revision-specific views | [Architecture](ARCHITECTURE.md) | Documented; identity algorithm open |
| C06 | Non-exclusive presence and intention tags | [Cooperation](AGENT-COOPERATION.md) | Documented |
| C07 | Concurrent proposals on shared elements | [Architecture](ARCHITECTURE.md) | Documented; merge protocol open |
| C08 | Interaction-triggered discussions | [Cooperation](AGENT-COOPERATION.md) | Documented |
| C09 | Counter-review at every scale, including the master | [Cooperation](AGENT-COOPERATION.md) | Documented |
| C10 | Master micro/macro evaluation and selection | [Cooperation](AGENT-COOPERATION.md) | Documented |
| C11 | RAM, persistence, recovery, and retrieval freshness | [Architecture](ARCHITECTURE.md) | Documented; storage choices open |
| C12 | Candidate filesystem projections, disk exports, and small sandboxes | [Validation](REQUIREMENTS-AND-VALIDATION.md) | Documented; isolation design open |
| C13 | Combined validation and evidence invalidation | [Validation](REQUIREMENTS-AND-VALIDATION.md) | Documented |
| C14 | Constraints, thresholds, optimization, and incompatible demands | [Requirements](REQUIREMENTS-AND-VALIDATION.md) | Documented |
| C15 | Requested performance/security/reliability variants and comparison | [Requirements](REQUIREMENTS-AND-VALIDATION.md) | Documented |
| C16 | Single-model, multi-model, and multi-provider scenarios | [Cooperation](AGENT-COOPERATION.md) | Documented; adapters unspecified |
| C17 | Source-file output without Git as the coordination engine | [Architecture](ARCHITECTURE.md) | Documented |
| C18 | Intermediate logical representation and target languages | [Research](RESEARCH-AND-ROADMAP.md) | Exploratory and deferred |
| C19 | Latent communication and internal model modification | [Research](RESEARCH-AND-ROADMAP.md) | Deferred |
| C20 | SHAPER responsibility mapping and contextual continuity | [Vision](VISION.md), [Continuity](CONTEXT-AND-CONTINUITY.md) | Conceptual mapping only |
| C21 | French conversation and English project artifacts | [Agent instructions](AGENTS.md) | Recorded rule |
| C22 | Concept illustrations | [Visuals](visuals/README.md) | Refreshed for the current concept; non-normative |
| C23 | Distinct containment, dependency, authority, and exploration relationships | [Architecture](ARCHITECTURE.md), [Foundations](SHAPER-FOUNDATIONS.md) | Documented |
| C24 | Prepared context and required context horizons by role | [Continuity](CONTEXT-AND-CONTINUITY.md), [Cooperation](AGENT-COOPERATION.md) | Documented |
| C25 | Conditional lessons and separation of observations from interpretations | [Continuity](CONTEXT-AND-CONTINUITY.md), [Foundations](SHAPER-FOUNDATIONS.md) | Documented |
| C26 | Observer limits, review effectiveness, and useful unexpected success | [Cooperation](AGENT-COOPERATION.md), [Validation](REQUIREMENTS-AND-VALIDATION.md) | Documented |
| C27 | Session, operation, attempt, causality, and interruption reconciliation | [Architecture](ARCHITECTURE.md) | Documented; protocol open |
| C28 | Visible, indexed, and managed files; distinct working views, candidates, and accepted states | [Architecture](ARCHITECTURE.md), [Foundations](SHAPER-FOUNDATIONS.md) | Documented; adoption protocol open |
| C29 | Bounded exploration and human controls independent of model availability | [Cooperation](AGENT-COOPERATION.md) | Documented; controls not implemented |
| C30 | Rust core, durable SQL, vector retrieval, and optional memory or graph services | [Research](RESEARCH-AND-ROADMAP.md) | Candidate comparison; no stack selected |
| C31 | Code decomposition from functions and methods to blocks, statements, expressions and tokens | [Architecture](ARCHITECTURE.md) | Documented; language adapters open |
| C32 | Line-level editing with separate identity, impact, and embedding scopes | [Architecture](ARCHITECTURE.md) | Documented; policies to evaluate |
| C33 | Master-only direct present reads and writes; coherent promotion | [Architecture](ARCHITECTURE.md), [Cooperation](AGENT-COOPERATION.md) | Documented invariant; enforcement unimplemented |
| C34 | Concurrent virtual source work in RAM and pinned FUSE-style candidate projections | [Architecture](ARCHITECTURE.md) | Documented; filesystem and sandbox design unqualified |
| C35 | Multi-move exploration graph distinct from code containment | [Architecture](ARCHITECTURE.md), [Vision](VISION.md) | Documented; search policy open |
| C36 | Scoped path assessments, search states, and non-transitive validation | [Validation](REQUIREMENTS-AND-VALIDATION.md) | Documented; evaluation unimplemented |
| C37 | Canonical vocabulary separating structures, mutable views, fixed candidates, and promotion | [Vocabulary](GLOSSARY.md) | Reviewed across project documents |
| C38 | Intent candidates before a usable code realization | [Architecture](ARCHITECTURE.md), [Research](RESEARCH-AND-ROADMAP.md) | Documented; no source tree created |
| C39 | Preserved SHAPER principles and evidence-based reassessment by future models | [Validation](REQUIREMENTS-AND-VALIDATION.md), [Foundations](SHAPER-FOUNDATIONS.md) | Documented; future gains unmeasured |
| C40 | DeepSeek Harness plugin integration with an external RARMURE service | [Research](RESEARCH-AND-ROADMAP.md), [Source study](DEEPSEEK-HARNESS-PLUGIN-STUDY.md) | Official repository cloned and interfaces inspected; no plugin or runtime qualification |
| C41 | Asynchronous parallel work, authorized per-role provider routing, and complementary review panels | [Cooperation](AGENT-COOPERATION.md), [Vocabulary](GLOSSARY.md), [Source study](DEEPSEEK-HARNESS-PLUGIN-STUDY.md) | Documented design; scheduling, routing, isolation, and benefits unqualified |

## Dependencies and decisions still required

The concept eventually needs an exact-content store, a transaction/revision mechanism, event delivery, source parsing or equivalent structure extraction, semantic indexing, provider adapters, an execution boundary, test tooling, and a human inspection interface. No product or library is committed for these responsibilities.

Research directions additionally need compatible models, access to suitable model internals, evaluation tasks, and resources. Their availability has not been established.

## Evidence status

| Dimension | Status |
| --- | --- |
| Documented | The capabilities above have conceptual coverage |
| Implemented | No application implementation |
| Runtime-tested | No runtime exists or has been tested |
| Deployed | No deployment |
| Benchmarked | No measured speed, quality, or cost improvement |
| Human-accepted | The concept is being developed with the user; this document set awaits their reading |

Documentation checks concern file presence, local links, image integrity, terminology, and concept coverage. They do not change runtime status.

### Delivery verification

The initial delivery contained 11 Markdown documents and 3 PNG illustrations, with 45 resolving local links and verified image integrity. The foundation study adds one Markdown document and extends the architecture, cooperation, continuity, validation, glossary, and coverage definitions. The illustrations are unchanged.

A documentation consistency review checked the recurring cooperation cycle, separate durable/retrieval responsibilities, deferred model research, variant comparison, and the expanded C01–C32 inventory. Governance, human use, and runtime failure were examined as three perspectives by the same assistant. This is not an independent agent review or a runtime test.

The present clarification extends coverage to C33–C36 and revises C03, C05–C07, C10, C12–C13, C17, and C28–C29. It distinguishes master promotion, virtual concurrent editing, candidate filesystem projections, and multi-move path assessment. Documentation checks cover local references and consistent authority terminology; no filesystem, sandbox, promotion protocol, or search algorithm has been implemented or executed.

The vocabulary review establishes [canonical terms](GLOSSARY.md) and updates technical prose and diagrams: code tree versus exploration graph, mutable working view versus fixed candidate, view issuance versus promotion, and empirical evidence versus formal proof. Assessment labels now state whether criteria were assessed and met; search status remains separate. C37–C40 cover these definitions, intent-first development, future-model reassessment, and the proposed harness integration. Retained images remain illustrative and may use earlier shorthand.

## Source coverage and delivery limits

The current visual refresh replaces the three illustration files, displays all three in the project README, and records their generation briefs and interpretation limits. The working title is **Real-Time Fractal Vibe Coding**: live coordination is a design intention, not a measured timing guarantee. This refresh concerns C02–C03, C09–C16, C20–C22, C33–C37, and C41; it introduces no runtime or benchmark evidence.

The parallel coordination extension covers C41: separate concurrent working views, bounded asynchronous work items, authorized provider routes, complementary candidate and master-selection reviews, and explicit handling of missing reviews and stale evidence. These are design contracts. Documentation verification does not establish concurrent execution, provider compatibility, or a speed gain.

The Harness study inspected the official source at `5badb15009ae1756c3afe0ae0cef1faafc290ccc`, including plugin tutorials, authoring practices, tool policy, agent context delivery, filesystem providers, packaging, presets, and Agent Teams limitations. The upstream checkout remains separate from the intended RARMURE repositories. No dependency installation, runtime launch, source modification, or provider call was performed for this study. Coverage concerns C05–C08, C11–C13, C16, C27, C33–C34, and C40; the remaining integration and enforcement questions are stated in the study.

The foundation study read 22 SHAPER OS V1.15 documents and 10 SHAPER Three Layers documents in full, including governing and navigation documents. It covered the OS rules, agent contracts, cognition, metacognition, cooperative ecology, six learning chapters, the three layer masters, object retrieval, synchronization, and conversational testing. The versioned references most relevant to the synthesis appear in [SHAPER foundations](SHAPER-FOUNDATIONS.md).

This is a focused study of the material relevant to collaborative code construction, not an exhaustive audit of either corpus. Historical context informs interpretation; current requirements and the proposed RARMURE contracts remain explicit. Reading a source does not adopt its technology profile or verify its implementation.

The images are preserved as visual development artifacts, with known interpretation limits stated alongside them. Their illustrative code paths, agent roles, and output extensions do not establish a chosen implementation.
