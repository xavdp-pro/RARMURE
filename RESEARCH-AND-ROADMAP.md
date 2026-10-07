# Research Boundaries and Possible Future Experiments

## Current decision

Preserve and formalize the concept. Internal AI coding behavior modification is beyond the currently available means and remains deferred. This document proposes future evaluation steps; it is not an instruction to start them or a claim that resources are available.

Start with intent candidates. Introduce source code only for a bounded implementation with a useful outcome and explicit validation criteria; do not create a placeholder source tree now. Preserve SHAPER principles and model-independent requirements so future models can reassess the design or improve an implementation under the same evidence discipline.

## Broader ambition and code-first qualification

RARMURE could investigate coordinated collective reasoning in domains beyond code: product conception, research, system architecture, and decision preparation. Shared intentions, fractal exploration, counter-review and retained evidence are potentially reusable mechanisms. Their benefit outside software remains a separate hypothesis.

Keep software construction as the first concrete laboratory. A broader direction must define the relevant objects, candidate artifacts, verification methods, uncertainty states and human acceptance criteria before an experiment is proposed. The [vision](VISION.md#collective-reasoning-beyond-code) and [verification boundary](REQUIREMENTS-AND-VALIDATION.md#verification-beyond-software) govern this distinction. This clarification authorizes no general-purpose platform implementation or non-code experiment.

## Practical baseline versus deeper research

| Direction | Meaning | Current status |
| --- | --- | --- |
| Explicit shared graph | Agents use ordinary interfaces to read objects and submit intentions and proposals | Concept defined; not implemented |
| Incremental source structure | Parse exact source and update structural relationships as it changes | Candidate technique; no parser selected |
| Concurrent contributions | Preserve candidate states and assess compatible combinations | Required behavior; write/merge algorithm unresolved |
| Present and candidate separation | Master-only direct present access; parallel virtual candidate changes in RAM | Required boundary; access and promotion protocols unresolved |
| Virtual filesystem projection | Expose pinned candidates through a FUSE-style mount for execution | Proposed bridge; implementation and isolation unqualified |
| Multi-move exploration | Compare transformation sequences using scoped evidence and bounded search | Required concept; scheduling and pruning policies open |
| Logical intermediate representation | Express operations, constraints, effects, and guarantees before target-language realization | Exploratory research |
| Latent agent communication | Transfer compatible model-internal representations | Deferred research |
| Model adaptation or training | Change a model's behavior to work natively in the environment | Deferred; resources and methodology unspecified |

## Candidate storage arrangement

### Harness integration candidate

DeepSeek Harness is a candidate host for agent execution because its [documented plugin architecture](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/architecture.md) exposes replaceable tools, model adapters, agent execution, filesystem capabilities, and events. A RARMURE plugin could connect those interfaces to a Rust service owning the active graph and to its durable and retrieval stores. The storage choices below remain separate from the choice of harness.

The plugin would adapt context, intentions, proposals, reviews, and experiment requests. The RARMURE service would enforce view permissions, exact revisions, and master-authorized promotion. Harness configurability does not establish that every filesystem or subprocess path obeys that contract. Qualification must cover attempted worker access to the present, view refresh, pinned test inputs, and interrupted operations. The documented [Agent Teams interface](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/agent-team.md) provides related coordination mechanisms, not RARMURE's complete exploration and revision model.

Start by evaluating extension points; change Harness source only if a concrete missing capability requires it. No plugin, database connection, or local Harness instance has been implemented or qualified for RARMURE.

The [source inspection study](DEEPSEEK-HARNESS-PLUGIN-STUDY.md) records the exact checked-out revision, external bundle creation path, tool and filesystem interfaces, MCP alternative, and shared-workspace limits of Agent Teams. Its evidence is source inspection, not runtime qualification.

### Storage candidates

Rust, MariaDB, and Qdrant are a candidate realization suggested during concept development on 2026-10-07. The following allocation is a design proposal, not a committed stack or a performance result.

| Responsibility | Initial candidate | Reason to evaluate it |
| --- | --- | --- |
| Active exact graph and candidate overlays | Native Rust data structures in one core service | Direct local traversal without a database RPC for each relationship |
| Durable revisions, decisions, operation journal and evidence metadata | MariaDB with InnoDB | Transactional persistence and recovery responsibilities |
| Semantic discovery | Qdrant | Vector search returning references to versioned code and context |
| Shared temporary state across services, if needed | Valkey or Dragonfly | Network-accessible in-memory structures |
| Declarative relationship queries, if needed | Memgraph or Neo4j | Query connected requirements, code, proposals, tests, and decisions |

[InnoDB](https://mariadb.com/docs/server/server-usage/storage-engines/innodb/innodb-storage-engine-introduction) supports transactions, row-level locking, and crash recovery. These properties are useful building blocks; the application still owns its revision and operation semantics. [Qdrant points](https://qdrant.tech/documentation/concepts/points/) combine vector data with IDs and payload. RARMURE would bind those IDs to source revisions and resolve exact content separately.

### Memory inside the Rust core

[SlotMap](https://docs.rs/slotmap/latest/slotmap/) offers versioned handles and constant-time object insertion, access, and removal. [Petgraph StableGraph](https://docs.rs/petgraph/latest/petgraph/stable_graph/struct.StableGraph.html) provides an adjacency-list graph with graph traversal support and indices unaffected by unrelated removals. These are candidate collections, not complete databases, concurrency protocols, or semantic identity systems. Persistent RARMURE object IDs must remain distinct from process-local handles and graph indices.

An initial design could share immutable base content, retain provisional changes in working views, and capture each candidate as a fixed revision. A bounded coordinator could validate and record revision transitions while analysis and experiments run concurrently. This is a starting design to measure, not a claim that a single writer or a particular collection will meet all future workloads.

### When a separate memory service helps

[Valkey](https://valkey.io/docs/topics/introduction/) provides in-memory structures, atomic operations, streams and optional persistence. [Dragonfly](https://www.dragonflydb.io/docs) is another in-memory store built around a multithreaded architecture. They become candidates when separate services need shared presence, short-lived coordination data, or caches. Their generic key/value access does not supply RARMURE's code relationship semantics.

Measure representative reads, multi-object changes, hot-object contention, memory use and recovery before selecting one. Vendor throughput figures are not RARMURE measurements. A separate service adds transport and serialization costs but can also provide operational capabilities otherwise requiring implementation.

### When a graph database helps

A graph database can answer questions such as: which active intentions affect callers of this function, which requirements depend on a changed interface, and which evidence is invalidated by a dependency revision? These follow typed relationships rather than vector similarity. [Neo4j's property graph model](https://neo4j.com/docs/getting-started/graph-database/) explicitly stores nodes, relationships, and properties.

[Memgraph](https://memgraph.com/docs/fundamentals/data-durability) is particularly relevant to the proposed in-memory direction: its transactional memory mode uses snapshots and write-ahead logging for recovery. It is a candidate graph service, not evidence that RARMURE's branching workload will be faster than native Rust traversal. Its configured durability and concurrent transaction behavior need qualification.

Two alternatives deserve comparison: a native Rust active graph with MariaDB persistence, or a Rust coordinator using a graph database for relationship storage and queries. A graph service can also be a derived query projection. If it is derived, expose its applied revision and lag; if it owns authoritative state, define that ownership and remove the competing owner. Avoid uncoordinated writes to several stores claiming to own the same revision.

[GraphQL](https://graphql.org/learn/introduction/) is an API query language and execution layer, independent of a particular database. It could expose selected project views to an interface or agents; it does not itself provide graph storage, transactions, or code conflict resolution.

### Durability before derived indexing

For the initial MariaDB-owned proposal, a durable revision and its pending indexing event would be recorded together in a transaction. The active graph and Qdrant would consume that committed sequence, with idempotent processing and visible revision watermarks. Provisional working views may be faster, but they must not be labeled durable before persistence succeeds. Database durability settings and recovery need explicit tests.

The [MariaDB MEMORY engine](https://mariadb.com/docs/server/server-usage/storage-engines/memory-storage-engine) loses table contents when the server restarts and is documented for temporary work areas or caches. It would not by itself satisfy the durable-source responsibility.

## A future logical representation

An intermediate representation might express inputs, decisions, effects, failures, and invariants while associating them with intent and evidence. An example operation could specify a transfer with positive amount, sufficient funds, conservation of total balance, and an all-or-nothing effect.

This is an illustrative direction, not an executable language specification. A target realization still has numerical, memory, concurrency, and error semantics. Those constraints cannot be discarded; they must be represented or resolved explicitly. Code generation must preserve the required meaning and be tested accordingly.

Retrieval vectors alone do not supply a lossless formal program representation. There is no demonstrated universal “AI-native vector language” in RARMURE.

## Latent communication

Direct exchange of model-internal representations is distinct from structured messages, RAG retrieval embeddings, or transmitting text through a different channel. It may require access to an inference engine and compatible internal representations. It does not necessarily require retraining in every research approach.

Cross-model interoperability, interpretability of decisions, source-object binding, persistence, and end-to-end benefit remain questions. Latent communication should not become a prerequisite for the explicit shared-memory concept.

## Related public work

These references were consulted during concept development on 2026-10-07. They are related mechanisms, not proof of the complete RARMURE system or selected dependencies.

| Reference | Relevance and limit |
| --- | --- |
| [Tree-sitter](https://tree-sitter.github.io/tree-sitter/index.html) | Incremental source parsing; syntax structure does not by itself establish program meaning |
| [Automerge conflict handling](https://automerge.org/docs/reference/documents/conflicts/) | Concurrent document changes and explicit conflicts; data convergence does not establish behavioral correctness |
| [PostgreSQL write-ahead logging](https://www.postgresql.org/docs/current/wal-intro.html) | Durable recovery principles; no storage selection has been made |
| [Redis persistence](https://redis.io/docs/latest/operate/oss_and_stack/management/persistence/) | Snapshots, journals, and durability/latency trade-offs |
| [LatentMAS paper](https://arxiv.org/abs/2511.20639) and [implementation](https://github.com/Gen-Verse/LatentMAS) | Research into shared latent collaboration without additional training in the described approach; published evaluations do not validate RARMURE |
| [GibberLink](https://github.com/PennyroyalTea/gibberlink) | Agents using a data-over-sound protocol; transport encoding is distinct from sharing internal representations |
| [Emergent communication research](https://ai.meta.com/research/publications/multi-agent-cooperation-and-the-emergence-of-natural-language/) | Learned communication in bounded cooperative tasks; not a universal programming language |

No external benchmark numbers are adopted as RARMURE performance targets or results.

## Possible future sequence

| Stage | Bounded question | Exit evidence |
| --- | --- | --- |
| 0. Concept | Are purpose, objects, boundaries, and unresolved choices explicit? | Reviewed documentation and coverage inventory |
| 1. Shared references | Can two workers resolve the same object through renames and fixed revisions? | Reproducible identity and stale-state examples |
| 2. Coordination | Can intersecting intentions trigger a useful review and discriminating test? | A recorded case that detects a real behavioral interaction |
| 3. Materialization | Can separate candidates and a combined state be executed reproducibly? | Exact manifests and reproducible local/combined results |
| 4. Recovery | Can durable state recover and stale retrieval be handled honestly? | Controlled interruption, replay, and freshness checks |
| 5. Selection | Can the master compare profiles and justify compatible choices? | Counter-reviewed decisions against explicit criteria |
| 6. Evaluation | Does the system improve accepted outcomes relative to a simpler baseline? | Comparable tasks, budgets, quality, time, and cost measurements |
| 7. Optional research | Does a logical representation or latent channel add value? | Separate experiments with compatible models and suitable resources |

The evaluation stage addresses the [collaboration hypothesis](REQUIREMENTS-AND-VALIDATION.md#collaboration-hypothesis-and-comparison): whether the shared representation and fractal exploration produce more useful coordination, within one provider or across several, than a comparable worktree-based orchestration. A speed gain is optional. Benefits, costs, and mandatory correctness constraints must be reported separately.

These are proposed phase exits, not completed milestones or a committed schedule. A useful first experiment would use two workers on one interacting behavior, rather than begin with a universal language.

## Open questions

- What is the right unit of code identity across languages and refactorings?
- How are inferred dependencies corrected and distinguished from verified structure?
- Which transformations can be combined automatically, and when must they be reviewed?
- How does master-authorized promotion change multiple objects coherently and reject stale master instances without long-lived exploration reservations?
- How are present read restrictions enforced across APIs, retrieval, mounts, and subprocesses while supplying useful worker views?
- Which FUSE and toolchain behaviors must a pinned candidate projection support, and how are writable outputs separated?
- How are search width, depth, and pruning chosen without confusing an unexplored continuation with a failed path?
- What evidence remains applicable after a dependency, requirement, or toolchain change?
- How are budgets allocated among exploration, counter-review, and validation?
- How does a project avoid endless branching or a master bottleneck?
- How much of the graph and retrieval index should remain in RAM?
- How are provider outages, capability differences, and authorized data boundaries handled?
- What is the smallest useful product that preserves the core idea?

The living-tree and mathematical-breathing metaphors guide design discussion. They are not proofs of convergence, optimality, correctness, or superiority.
