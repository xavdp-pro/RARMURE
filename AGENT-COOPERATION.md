# Agent Cooperation and Counter-Review

## Roles rather than territories

Workers investigate and propose. Reviewers challenge assumptions and evidence. Executors run bounded experiments. The master coordinates requirements, interactions, and selection. These roles can be implemented by different agents or scheduled sessions; assigning a role does not grant unlimited authority.

Agents can share a code element. Their identity and intention tags signal activity and expected effects. They do not lock the object or make the first agent its owner.

Only the master has direct agent access to the canonical present, for both reading and writing. Workers, reviewers, and subordinate coordinators use issued bases and virtual working views. They may explore the same elements concurrently in RAM. Local coordination does not confer authority to advance the canonical present through promotion; the runtime enforces this boundary beyond prompt instructions. See [present authority](ARCHITECTURE.md#present-authority-and-virtual-exploration).

## Parallel exploration and scheduling

Parallel work is a first-class design requirement. Several workers may explore different solutions to one requirement, different interacting elements, or successive moves on different exploration paths. Two workers targeting the same function receive separate mutable working views from an identified base; neither overwrites the other's work. A composition creates another candidate with explicit contributing revisions and assumptions.

A scheduler dispatches bounded work items rather than serializing every action through the master. Each item records its role, objective, dependencies, issued view/base, provider route, allowed tools, required evidence, resource budget, and stop conditions. Ready work proceeds asynchronously. Coordination occurs at relevant intention changes, dependency boundaries, candidate capture, review, and selection; it does not require a global discussion after every edit.

Concurrency limits apply per provider, execution environment, and project budget. Cancellation, retries, duplicate delivery, and stale results must preserve operation identity and attribution. A result obtained from an older base remains attached to that base until its applicability is reassessed. The master can redirect or prune exploration without discarding its recorded evidence. The number of workers and exploration depth adapt to useful progress and available resources; more agents do not establish faster completion.

## Intention registration

Before substantial work, a worker should register an intention containing:

- Its agent/session identity and current role.
- The objective and linked requirements.
- Target object IDs, relevant dependencies, and base revisions.
- Assumptions, expected effects, and likely interaction points.
- Planned evidence, resource bounds, and stop conditions.

An intention can evolve. Updates should explain a material change in scope or assumptions. Folder-level summaries help navigation, while element-level references support precise coordination.

Each role receives a prepared, bounded context with source revisions, applicable mandates, dependency assumptions, open objections, missing information, and expected evidence. Required context may span the immediate input, current session, system relationships, or accumulated use. A role that needs a wider horizon requests the relevant material within its data boundary. Reasoning capability does not compensate for absent context; see [Context and continuity](CONTEXT-AND-CONTINUITY.md).

## What triggers a discussion

The system should initiate targeted coordination when a change affects another active intention or invalidates an assumption. Candidate triggers include:

| Trigger | Example |
| --- | --- |
| Overlapping transformations | Two agents alter one function's return behavior |
| Dependency change | A caller's expected interface changes in another file |
| Requirement tension | A speed optimization weakens an access-control guarantee |
| Combined-test failure | Individually passing changes fail when assembled |
| Stale evidence | An accepted dependency changes after a test run |
| Reviewer objection | A relevant failure case is missing from the proposed validation |

Editing the same file is useful evidence of possible interaction, but is neither a necessary nor sufficient condition for a semantic conflict. Notifications use current events and relationships; they do not wait for vector reindexing.

## A discussion produces an actionable record

Participants receive the requirements, exact affected revisions, assumptions, proposals, and available evidence. The useful outcomes are a revised proposal, a discriminating experiment, an explicit compatible combination, a retained alternative, or a documented unresolved question.

Agreement records identify the participating contributions and scope. Agreement alone is not proof. A disagreement should remain visible until resolved, deferred with a reason, or escalated within the human-defined authority boundary.

The discussion protocol should bound repeated debate. When progress stops, participants should identify the missing evidence or decision instead of generating unlimited arguments. Human clarification is appropriate for a genuinely ambiguous requirement or an unmandated trade-off.

Separate the observed discrepancy from proposed explanations. Attach discussions to exact code and requirement references so their decisions remain discoverable after a rename or session change. A minority objection remains assessable on its evidence. Useful unexpected success can also trigger investigation; coordination should discover improvements as well as defects.

## Counter-review in every cycle

Every substantive working cycle includes a separate reviewing role. Review should test a claim, not merely paraphrase it. Typical questions are:

1. Which assumption could make this proposal fail?
2. What relevant counterexample is missing?
3. Does the evidence assess the exact proposed revision?
4. Which callers, data states, or concurrent operations could be affected?
5. Does a local improvement damage a global requirement?
6. What experiment could distinguish the competing explanations?

Where feasible, the reviewer forms an initial assessment from the requirements and candidate before seeing the author's conclusion. This aims to reduce anchoring; it does not guarantee independent judgment. Review depth should match the impact of the change, and unchanged review results can be reused only when their validity conditions still hold.

Reviewers can disagree, and master decisions receive their own counter-review. Escalating a material unresolved objection is more useful than an infinite chain of reviewers reviewing reviewers. The future system needs an explicit termination and escalation policy.

Assess the reviewer through its observable consequences: detected defects, missed interactions, unnecessary blocking, and regressions caused by its advice. A reviewer may challenge a test or criterion, but changing an authoritative requirement is a separate decision. Self-review under another role name must not be presented as an independent counter-view.

### Multiple complementary counter-reviews

A substantive candidate may receive a review panel: several bounded reviewing roles with complementary questions, rather than one generic approval. Example perspectives include behavioral correctness, security, performance, and integration with the wider specification. The required perspectives depend on the change and its requirements; every small edit need not invoke every specialist.

Reviewers assess the same fixed candidate and identified criteria. Where feasible, their initial assessments are produced separately before exchanging conclusions. They then compare concrete objections, evidence, and proposed discriminating experiments. Each review records its coverage, assumptions, unresolved objections, and model/provider provenance. Different providers may broaden perspectives, but do not establish independent errors. A missing or unavailable required review remains visible as missing coverage.

Review rounds have a budget and a termination rule: resolve material objections through revision or evidence, retain alternatives, or record an unresolved decision for the appropriate authority. A candidate change creates a successor; earlier reviews carry forward only where their validity conditions hold. A majority vote cannot discharge a mandatory requirement. The master's proposed selection and trade-offs also receive complementary counter-reviews before promotion, within the same bounded process.

## The master's micro and macro views

| View | Questions |
| --- | --- |
| Micro | Does the behavior work? Are contracts and dependencies consistent? What do tests actually establish? |
| Macro | Does the whole meet the specification? Are local gains compatible? Which global trade-offs remain? |

The master maintains an up-to-date overview of candidate states, evidence freshness, requirements coverage, disagreements, and resource consumption. It can direct attention toward an untested assumption, select compatible options, or retain several valid realizations.

The master does not choose a candidate because it has the most votes or the most confident explanation. It records criteria and evidence. Its proposed selection is counter-reviewed, then the combined realization is validated. Changed human priorities may justify reopening an earlier choice.

The master also compares paths several moves ahead. It records which continuations are worth exploring, which exact checkpoints meet their criteria, and which are rejected under stated conditions. A promising continuation is not a validated result. A reviewer receives a fixed candidate issued for review and relevant evidence, without direct access to the present. Only an explicit master promotion advances the present; a `meets_criteria` assessment or completed worker task cannot do so.

## Fractal coordination

Subsystem coordination can repeat the same pattern within a bounded scope. Local acceptance must state what it assumes about the surrounding system. Parent-level validation assesses those assumptions and interactions.

The global master need not approve every small experimental step. Its responsibility is coherent selection and visibility across the authorized project, including failures that span local boundaries. The number of agents, recursion depth, and scheduling policy remain design questions.

Each active scope should declare resource bounds, a progress signal, stop conditions, and a condition for resumption. Repeated work with no new observation, hypothesis, or useful artifact calls for a change of method, a pause, or a bounded unresolved result. A candidate's failure does not make its author permanently unsuitable; capability assessments must retain task and context conditions.

## Human control and runtime continuity

The human should be able to inspect accepted source, stop exploration, revise priorities, and revoke a mandate through ordinary runtime controls when a model is unavailable. Routine actions inside a valid mandate need no repeated approval. Scope expansion and requirement changes follow their actual authority boundary.

Separate experiments on candidate code from repair of the live infrastructure sustaining RARMURE. A test candidate must not replace that infrastructure merely because it passes its own checks. Recovery of compromised supporting components needs a control path outside the component being repaired. The concrete recovery topology remains open.

## Single-model, multi-model, and multi-provider operation

The concept should accommodate:

- Several roles using one model at one provider.
- Several models at one provider.
- Several models across different providers.
- A future mix of locally hosted and remote models.

A common explicit protocol carries object references, requirements, intentions, proposals, observations, reviews, and decisions. Adapters translate that protocol into each model's supported interface. The system should record model/provider identity and relevant execution settings for reproducibility and review context.

Provider diversity may produce useful counter-views, but it is not proof of independent errors. Capability differences, permissions, quotas, confidentiality constraints, latency, cost, and unavailable providers must be represented rather than hidden.

A **provider route** binds an agent work item to an allowed provider, model, relevant execution settings, and data policy. Routes can differ between workers, specialist reviewers, and the master; several agents may also use the same route. Changing a route must preserve the task contract and record the actual execution identity. Fallback is permitted only to an authorized route satisfying the required capabilities and data boundary; it must not silently widen access or replace an unavailable required review with an assumed approval.

Provider adapters handle each supplier's interface. The scheduler controls dispatch and budgets; the RARMURE service controls project state and view authorization. Suppliers receive only issued context permitted for their route. Neither a provider connection nor a reviewing role grants access to the canonical present.

Ordinary structured agent interfaces are the conceptual baseline. Direct transfer of latent model states requires additional compatibility and evaluation work and remains deferred. A shared RAG embedding does not make arbitrary models' internal states interchangeable.
