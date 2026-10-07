# Requirements, Selection, and Validation

## The common objective

Every exploration path should connect to the human specification, a necessary dependency, or an explicitly authorized investigation. Requirements need stable identities and revisions so that evidence can be interpreted against the right demand.

Words such as “extreme performance,” “high security,” and “high reliability” express direction but do not yet define acceptance. They must be translated into conditions and observable criteria.

| Requirement class | Meaning | Illustrative example |
| --- | --- | --- |
| Mandatory constraint | Must hold for an acceptable realization | An unauthorized operation must be rejected |
| Acceptance threshold | Required measured behavior in stated conditions | Response latency remains below a defined bound at a specified load |
| Optimization preference | Improves selection among acceptable realizations | Lower memory use when required behavior and latency are preserved |

Other dimensions may include cost, energy, maintainability, simplicity, accessibility, privacy, compatibility, explainability, portability, and delivery time. This list is extensible.

## Trade-offs and incompatible demands

Some changes improve several dimensions together. Others create tensions. The master should compare measured behavior rather than assume that every improvement requires a trade-off.

First assess mandatory constraints and thresholds. Then compare optimization preferences, including the conditions and uncertainty of each measurement. Several non-dominated candidates may remain: improving one dimension would worsen another among the options currently known. This is a practical set of alternatives, not proof of global optimality.

Do not hide a violated mandatory constraint inside an aggregate score. If the requested combination appears infeasible, state the search performed, what failed, what remains unknown, and which changes to the demand would make progress possible. A finite unsuccessful search does not prove impossibility.

## Requested variants and fair comparison

A user could request a performance-oriented realization and a security-oriented realization of the same program. Each request defines a selection profile over the shared specification; it does not waive mandatory requirements.

For a performance-oriented profile, specify workload, environment, latency or throughput objective, resource limits, and retained correctness constraints. For a security-oriented profile, specify assets, threat model, trust boundaries, required controls, and operational constraints. Reliability-oriented profiles likewise require defined failure conditions and recovery objectives.

Evaluate the retained variants across the relevant common criteria. Record exact revisions, comparable environments, experimental conditions, and measurement uncertainty. Some checks may be profile-specific, but their different coverage must remain visible. Security has no universal scalar score, and “fastest” is meaningful only relative to the candidates and conditions assessed.

The comparison should expose both benefits and costs rather than label every selected profile “best.” A user may choose one realization, retain several, or revise the priorities. Switching a profile can invalidate the prior selection rationale even when the underlying test observations remain valid.

## Three validation scopes

| Scope | Purpose | Limitation |
| --- | --- | --- |
| Individual sandbox | Test a worker's fixed candidate against targeted criteria | Does not establish compatibility with other contributions |
| Combined sandbox | Assemble selected changes and examine interactions | Does not establish every whole-system property |
| Project acceptance | Assess the selected realization against the specification in appropriate conditions | Some requirements need human judgment or real-environment qualification |

“Mini” means deliberately scoped and resource-bounded. It does not mean that important dependencies can be silently omitted or that a small sandbox provides perfect isolation. The implementation would need a concrete execution boundary, resource controls, data policy, and lifecycle management.

Test instances should be disposable and reproducible. External side effects require explicit scope and suitable controls. Synthetic fixtures and mocked dependencies must be labeled, with the resulting evidence limits recorded.

## Evidence records

Each experiment should identify:

- Requirement IDs and specification revision.
- Exact source and dependency state, including the candidate manifest.
- Environment, toolchain, configuration, and materialization versions.
- Inputs, workload, fixtures, assumptions, and relevant randomness.
- Checks performed, observations, result, and known coverage gaps.
- Executor identity, timing, and retained diagnostic artifacts.

An evidence record remains a historical observation. Its applicability may become stale when relevant source, requirements, dependencies, or conditions change. Determine which checks need rerunning from those relationships; do not display old success as current validation.

Counter-review can identify a missing test, but it cannot substitute for running that test. A passing test establishes the observed result under the recorded conditions rather than universal correctness.

Record observer limitations as part of the evidence: unavailable dependencies, stale fixtures, inferred relationships, measurement noise, and untested conditions. Unknown, unavailable, forbidden, infeasible, and failed are different states. A missing result must not be converted into either success or a prohibition.

Tests should examine both rejected invalid behavior and preserved legitimate behavior. A protection that blocks every request cannot qualify by passing only denial tests. When a defect is corrected, preserve a relevant regression case and revise the owning intent or invariant if its specification caused the defect. Changing a requirement or test solely to make a candidate pass requires explicit justification and the appropriate authority.

## Candidate maturation

### Path assessment and search state

Path labels have two independent dimensions. Search state can be `unexplored`, `active`, `paused`, or `pruned`. Assessment can be `unassessed`, `inconclusive`, `meets_criteria`, `fails_criteria`, or `stale`. Pruning means stopping expenditure under a recorded policy; it does not by itself establish a defect.

| Assessment | Required interpretation |
| --- | --- |
| `unassessed` | No assessment has yet been performed for the named criteria |
| `inconclusive` | An assessment was attempted, but its evidence is insufficient to conclude |
| `meets_criteria` | A named checkpoint meets named criteria under recorded conditions and evidence limits |
| `fails_criteria` | A named checkpoint or transition violates a criterion under stated conditions, with a reason or counterexample |
| `stale` | Previous evidence no longer establishes the assessment for the current conditions |

A record identifies the candidate, path or transition, requirement revisions, assessed scope, evidence, reviewer, assumptions, and next useful experiment. A path can contain both validated checkpoints and unexplored continuations. Validation of one node does not validate descendants, the whole path, or a composition with another candidate. Distinguish endpoint validity from transition validity when intermediate compatibility or migration matters.

Labels support bounded lookahead comparable to examining several chess moves, but program behavior is not a fully known game position. Heuristic ranking directs experiments; it does not prove an optimal path. A rejected intermediate can have a repaired successor. Dependency or requirement changes require reassessment without erasing historical results.

### Promotion boundary

Only the master can promote the selected state as the present. The runtime checks the exact assessed revisions, applicable validation, master authority, and expected prior present before a coherent durable transition. Tests read fixed candidate projections, never the moving present. Mounting a candidate, completing a test, or obtaining agent agreement does not promote the candidate.

Future qualification must demonstrate denied worker reads and writes to the present, stable mount content while exploration advances, view-scoped write capture where supported, rejection of stale promotion, and recovery without a partially visible present.

### Maturation sequence

The following sequence describes an intended workflow, not one field combining all statuses:

**Proposed → explored → locally tested → counter-reviewed → selected → jointly validated → accepted within scope.**

A fixed candidate may be reassessed or retired; editing it produces a successor candidate. Exploration paths may pause or resume. Record why a path was abandoned and retain useful evidence. An accepted snapshot is fixed; further edits in a working view create a new candidate rather than changing the meaning of the old acceptance.

Promotion, deployment, and human acceptance are separate transitions with their own applicable requirements. Selecting code inside RARMURE is not an implicit production deployment.

## Worked example: validation and performance

This example is hypothetical and reports no executed test.

Two agents work on one order-processing operation:

- Agent A adds a rule requiring a current authorization check.
- Agent B accelerates repeated work by introducing caching.

Their local tests pass in the imagined scenario. The graph detects that both changes affect the authorization path. A reviewer asks whether a user whose permission was revoked could still obtain a cached authorized result.

The coordinated experiment would process a request, revoke permission, and repeat the request against the combined candidate. If it succeeds when it should be denied, the combined proposal fails the mandatory constraint even if latency is excellent.

Possible refinements include caching only permission-independent computations or introducing a justified invalidation mechanism. Each option must be tested for its own correctness and failure modes. The master compares compliant candidates using workload, latency, resource cost, and maintainability evidence.

The chosen option is tested with the rest of the selected project state. The other option may remain useful under different operating assumptions.

## What “this path is valid” means

It means: **this fixed realization satisfies these stated criteria under these recorded conditions, with these evidence limits**.

It does not mean all alternatives have been explored, every future condition is covered, or the realization is the unique best solution.

## Performance claims about RARMURE itself

### Reassessment with future models

Keep intent, requirement revisions, acceptance criteria, prior candidates, decisions, and their evidence available independently of a particular model session. A later model can propose a successor from this retained context. It must not silently rewrite the requirements or replace the present.

Compare old and new realizations under explicit criteria and comparable conditions, including regressions, resource cost, and counter-review. A newer model may improve a result, leave it unchanged, or make it worse. Promotion follows the same authority and assessment contract. A six-month horizon is a design scenario, not a forecast, scheduled task, or automatic regeneration policy.

### System evaluation

A future evaluation should measure time to an accepted correct change, regression rate, review effectiveness, total model/tool cost, RAM usage, indexing delay, restart recovery, and coordination overhead. Compare equivalent tasks, requirements, and resource budgets against a simpler baseline.

Faster memory access alone does not establish a faster end-to-end workflow. Model inference, repeated debate, and test execution may dominate. No speedup or quality improvement has been established for RARMURE.

Evaluate context history, semantic retrieval, and provider diversity separately when practical. Compare the same scope with and without each contribution, preserving comparable budgets and acceptance criteria. Measure useful discoveries and unnecessary blocking as well as detected regressions. Token throughput and agent activity are intermediate measurements; the intended outcome is a correct, useful change accepted within scope.
