# RARMURE Vocabulary

This glossary defines the canonical English terms used in RARMURE. Each term identifies a structure, state, action, role, or assessment. The living-tree metaphor remains useful for explanation; technical contracts use the distinctions below.

## Structures and routes

| Term | Meaning | Boundary |
| --- | --- | --- |
| Code tree | Containment structure of code elements within one identified revision: folders, files, functions, blocks, and finer elements | Describes program structure, not possible futures or agent delegation |
| Dependency graph | Typed relationships such as calls, data access, requirement coverage, and test dependencies | Distinguishes established relationships from agent-inferred ones |
| Exploration graph | Candidate states connected by moves and composition relationships | Describes possible development histories; not necessarily a tree |
| Active graph | The portion of RARMURE's objects and relationships currently loaded in RAM | A storage/runtime term, not another name for the present |
| Exploration path | An ordered sequence of moves from an identified base through candidate states | Use the full term where a file path or execution path could be confused with it |
| Exploration fork | A point where two or more alternative continuations are considered | Does not create a Git branch or delegate an agent automatically |
| Move | A transformation connecting candidate states; a proposed move names a possible transformation before its result exists | Describes a change, not a state, token, or participant |
| Checkpoint | A fixed candidate chosen as a point of assessment along an exploration path | Being a checkpoint says nothing about whether its checks passed |
| Composition | An explicitly constructed candidate combining identified contributions | Requires its own assessment; does not inherit the success of its inputs |

The unqualified word **branch** is reserved for the visual metaphor. Use **code subtree** for containment, **exploration fork** for divergence, **exploration path** for a sequence, **working view** for editable context, and **delegation scope** for a subagent's mandate. When discussing an external system, qualify its own term, such as **Git branch**.

## States and views

| Term | Meaning | Boundary |
| --- | --- | --- |
| Present | The canonical project state designated by the current present revision | Only the master has direct agent read/write authority; human controls and trusted runtime services retain their defined roles |
| Present revision | The exact revision currently designated as the present | Changes only through promotion; old revisions keep their identity |
| Revision | An immutable, identified state of an object or project | Identity does not establish durability, correctness, or acceptance |
| Snapshot | A fixed capture of identified revisions for reconstruction, assessment, or delivery | Must be labeled durable only after persistence acknowledgment |
| Base snapshot | The fixed starting state from which a working view or exploration path derives | Remains identifiable when the present advances |
| Working view | An authorized base snapshot plus provisional changes being developed in RAM | May evolve; not a reproducible test input until captured as a candidate |
| Candidate | A fixed, identified proposed project state, possibly reconstructed from a base and recorded changes | May be incomplete or fail to compile; further edits create a successor candidate |
| Intent candidate | A fixed proposal for requirements, behavior, or design before source realization | Can be reviewed but cannot be reported as an executed program |
| Code candidate | A fixed candidate containing exact source | Source existence does not establish usability or acceptance |
| Candidate view | An authorized projection of a fixed candidate's content and context | A way to access a candidate, not an independently mutable state |
| Candidate manifest | Exact references describing a candidate and the dependencies, configuration, and toolchain needed for a specified experiment | A reference record, not the files or test result themselves |
| Realization | General prose for a concrete software construction | In state records, name the candidate and its explicit assessment or acceptance status |

**Live** means changing over time; it does not mean canonical. **Virtual** means represented through RARMURE's in-memory objects and views; it does not mean an embedding, a virtual machine, or direct access to a model's internal states. **Shared** does not grant every role access to every object.

## Actions and authority

| Term | Meaning |
| --- | --- |
| Intention registration | Record an agent's objective, targets, assumptions, and planned effects for authorized participants |
| Proposal | A request for a transformation, with a known base, target objects, assumptions, and expected effects; it may link to a resulting candidate |
| View issuance | Give an authorized participant access to a scoped base snapshot, candidate view, or working view |
| Selection | Choose candidate contributions for a next experiment or decision under stated criteria |
| Promotion | The master-authorized, coherent transition from the current present revision to an exact selected candidate |
| Materialization | Expose exact candidate content as ordinary files, through a filesystem projection or a disk export |
| Filesystem projection | A mounted file view pinned to a candidate manifest, potentially served through FUSE |
| Disk export | Write an identified state into ordinary persistent files |
| Deployment | Install or activate software in a target operational environment |
| Delegation scope | The bounded task, authority, data access, and resource budget given to a participant |

Use **promotion**, not **publication**, for advancement of the present. Use **register**, **issue**, **expose**, or **export** for the other actions above. External release publication must be named explicitly. A mounted candidate is neither promoted nor deployed merely because tools can see its files.

## Assessment and decisions

| Term | Meaning |
| --- | --- |
| Evidence | An attributed observation tied to exact revisions, conditions, and limitations |
| Qualified observation | An evidence record whose scope, observer, and limits are explicit |
| Validation | Assess specified criteria for an identified state using relevant checks and evidence |
| Combined validation | Assess a composition for interactions between its contributions |
| Acceptance | An explicit judgment by an authorized role that an identified state meets a stated acceptance contract within scope |
| Human acceptance | Acceptance made by a human, distinct from an agent's assessment or delegated acceptance |
| Counter-review | A distinct reviewing role challenging assumptions, claims, evidence, and decisions; separate role labels alone do not prove reviewer independence |
| Pruning | Stop spending search resources on a continuation under a recorded policy; does not establish that it is incorrect |

Search state and assessment are independent. The canonical search labels are `unexplored`, `active`, `paused`, and `pruned`. Assessment labels are `unassessed`, `inconclusive`, `meets_criteria`, `fails_criteria`, and `stale`; their exact meanings are defined in [Requirements and validation](REQUIREMENTS-AND-VALIDATION.md#path-assessment-and-search-state).

**OK** and **not OK** are conversational shorthand for scoped assessments, not unrestricted correctness claims or promotion instructions. **Tested** means checks ran, not that they passed. **Validated** must name the criteria, revision, and conditions. Use **evidence** for empirical observations; reserve **formal proof** for a demonstrated claim under explicit formal assumptions. **Promising** is a heuristic judgment used to direct exploration.

## Participants and supporting concepts

| Term | Meaning |
| --- | --- |
| Agent | An identifiable participant acting through bounded roles and interfaces |
| Master | The role coordinating micro/macro assessment and holding exclusive direct agent authority over the present; not an omniscient model or the persistence engine |
| Worker | A role investigating and proposing changes through authorized working views |
| Reviewer | A role challenging identified claims and candidates through issued context |
| Review panel | Several reviewing roles assessing complementary criteria on an identified fixed candidate or selection; agreement is not proof |
| Provider route | An authorized binding of a work item to a provider, model, execution settings, and data policy |
| Work item | A bounded assignment identifying a role, objective, view/base, dependencies, provider route, budget, and expected evidence |
| Executor | A bounded process or agent role running an identified experiment and returning evidence |
| Presence tag | A temporary, non-exclusive indication of activity; grants neither ownership nor permissions |
| Intention | A declared objective, scope, assumptions, and expected effects |
| Sandbox | A bounded execution environment for a specified candidate; filesystem exposure alone does not provide complete isolation |
| Semantic reference | A stable logical object identity plus an explicit authorized resolution mode |
| Semantic index | A derived retrieval structure mapping semantic similarity to exact object and revision references |
| RAG | Retrieval-augmented generation: supplying a model with relevant retrieved context |
| Durable memory | Acknowledged persisted source, events, decisions, evidence, and associated records |
| Lesson | A revisable interpretation of evidence with explicit applicability conditions |
| Context horizon | The scope of information needed for a judgment, from immediate input to accumulated use |
| Shared specification | Human-defined purpose, requirements, constraints, and acceptance criteria |
| Latent communication | Research into exchanging compatible model-internal numerical representations |

**Semantic pointer** is an explanatory alias for **semantic reference**, never a C address or an embedding. **Fractal parallelism** describes a cooperation pattern recurring at several scales. **Mathematical breathing**, **living tree**, and **functional beauty** remain design metaphors, not claims of mathematical convergence or measured correctness.

## Descriptive terms

**Concurrent exploration without ownership locks** means agents do not reserve code elements against others' exploration. It does not imply a **mutex-free**, **lock-free**, or **wait-free** implementation. Internal synchronization and coherent revision transitions remain separate design questions; master authority alone establishes no progress guarantee.

**Real-Time Fractal Vibe Coding** is RARMURE's working descriptive title. **Vibe coding** here means human intent guiding agent-assisted software construction, with explicit requirements, counter-review, and validation. **Fractal** names recurrence of that cycle across scales. **Real-time** names intended live coordination during work, not a measured latency guarantee or a completed runtime. Exploration forks and paths remain the precise terms for alternative futures; the title does not replace them.

## Worked vocabulary example

The master issues base snapshot `B0` derived from present revision `P0`. Worker A develops working view `W1` and submits proposal `Q1`. Capturing its changes produces candidate `C1`; the corresponding move connects `B0` to `C1`. A later move produces `C2`, forming an exploration path with two moves. Neither candidate is the present.

The executor receives a filesystem projection pinned to `C2` and records evidence. A reviewer assesses the stated criteria. The master may select `C2` and, after the applicable acceptance contract is satisfied, authorize promotion. A durable transition then designates that candidate as present revision `P1`. Worker B's working view derived from `B0` remains on its original base until an explicit successor or rebase is created.

This example assumes code candidates exist. Before that stage, exploration operates on intent candidates; no executable code tree is implied.
