# DeepSeek Harness Plugin Study

Inspection date: 2026-10-07. Upstream: [deepseek-ai/deepseek-harness](https://github.com/deepseek-ai/deepseek-harness). Inspected commit: `5badb15009ae1756c3afe0ae0cef1faafc290ccc`; checkout manifest version: `0.2.1-alpha.1`.

DeepSeek Harness provides the extension interfaces needed to begin designing a RARMURE adapter without first changing its agent loop. Its plugin system can expose tools, connect external services, contribute context, restrict tool access, and replace filesystem and execution providers. RARMURE's exact-state and authority rules still need their own implementation and qualification.

The repository was cloned and its documentation and selected source files inspected. Dependencies were not installed, Harness was not launched, and no plugin was implemented or tested. The checked-out source is pre-stable; compatibility with a later installed release must be checked against that release.

## How to create an external plugin

The official [first-plugin tutorial](https://github.com/deepseek-ai/deepseek-harness/blob/5badb15009ae1756c3afe0ae0cef1faafc290ccc/docs/user/develop/basic/index.md) uses a TypeScript module exporting `apply(ctx)`. Optional `inject` lists the services required before activation. Cordis also accepts object plugins and service classes.

For a model-facing tool, import `defineTool` from `@deepseek-ai/dsh-tools`, declare `inject = ['tools']`, and register it with `ctx.tools.register()` inside `apply`. Define its argument fields, canonical JSON output schema, model-facing rendering, and execution callback. `execute(args, exec)` receives validated arguments, caller context, and cancellation. Return the canonical value; let `output.render` turn it into model-facing content. The [tool tutorial](https://github.com/deepseek-ai/deepseek-harness/blob/5badb15009ae1756c3afe0ae0cef1faafc290ccc/docs/user/develop/basic/tool.md) and [authoring reference](https://github.com/deepseek-ai/deepseek-harness/blob/5badb15009ae1756c3afe0ae0cef1faafc290ccc/docs/cookbook/adding-a-tool.md) are the starting examples.

Expose deployment settings through an exported `Config` type and schema. The [configuration tutorial](https://github.com/deepseek-ai/deepseek-harness/blob/5badb15009ae1756c3afe0ae0cef1faafc290ccc/docs/user/develop/basic/config.md) uses `@deepseek-ai/schemastery`. A RARMURE adapter would need configurable service location, timeouts, and acquisition limits. Secrets should be referenced through the host's credential mechanisms rather than copied into a distributable patch.

Register connections and subscriptions as context-owned effects, with cleanup on unload. Per-agent registrations on `agent.ctx` also need their disposers owned by the parent plugin so unloading either owner removes them. Plugin replacement must not leave duplicate notifications or stale role authority behind.

### Local development versus distribution

A local source overlay inserts a uniquely identified plugin row. The first-plugin tutorial uses an absolute source path and starts a built checkout with `pnpm dsh web --patch <overlay>`. Merely cloning the repository is insufficient: the official source workflow first installs dependencies and builds the runtime. Those steps were not run in this study.

An installable bundle is a package whose `package.json` declares `dsh.bundle.patch`, pointing to a YAML layer that inserts or overrides plugin rows. A package without that declaration is a library dependency and activates no bundle layer. A profile names the ordered bundles composing an application. These are different concepts. See the [package-and-install tutorial](https://github.com/deepseek-ai/deepseek-harness/blob/5badb15009ae1756c3afe0ae0cef1faafc290ccc/docs/user/develop/basic/publish.md).

A proposed external package could contain:

```text
rarmure-harness-plugin/
  package.json
  cordis.patch.yml
  src/index.ts
  lib/index.js
  locale/en.json
  icon.svg
```

This is an illustrative package layout, not a created source tree. Runtime exports would point to built JavaScript. Declare shared Harness runtime packages as compatible peers, with development dependencies for type checking and tests; do not publish monorepo-only `workspace:*` dependencies in an external package. The inspected workspace's version does not establish that matching artifacts are currently available from a package registry.

For a future installation, use a dedicated profile instead of changing an existing working profile. The official CLI supports `dsh plugin --profile <name> add <package-path>`, followed by `dsh --profile <name> --dump-config`. The graphical Plugin Manager manages the same profile composition. Installation and activation outcomes must both be inspected.

Prefer a built package tarball for an initial external adapter. A Git-hosted TypeScript installation needs a self-contained build path and installation-time script approval; a source repository alone does not provide `lib/` artifacts. Patches replace an overridden row's complete configuration instead of merging selected keys. Higher-priority home or invocation patches can override a bundle. Configuration HMR and JavaScript module replacement have different restart behavior; verify the actual installed composition.

## RARMURE capability mapping

| RARMURE responsibility | Inspected Harness interface | Additional work |
| --- | --- | --- |
| Read authorized working or candidate views | Custom tools registered on `ctx.tools` | Resolve object IDs and exact view revisions in the RARMURE service |
| Register intentions and submit proposals | Custom tools with structured values | Enforce caller permissions, operation IDs, and stale-base handling |
| Supply role-specific context | `ctx.systemPrompt.section()` and `agent.inject()` | Retain exact source references and record model-visible inputs |
| Deny unauthorized operations | Scoped tool restrictions and `ctx.tools.guard()` | Enforce the same rules in the service and execution environment |
| Replace ordinary file access | A `FileSystem` provider on `ctx.fs` | Translate view/object/revision references into the provider's file operations |
| Execute fixed candidates | Filesystem/subprocess/sandbox capability composition | Supply pinned projections and separate writable outputs |
| Coordinate work and objections | Agent lifecycle events, subagent interfaces, optional Team messaging | Associate participants with views and preserve RARMURE's exploration graph |
| Inspect the exploration graph in the UI | A separate Client plugin using host slots/projections | A usable graph view and its transport; no UI has been built |

Proposed tool names include `rarmure_read_node`, `rarmure_register_intent`, `rarmure_submit_proposal`, `rarmure_capture_candidate`, and `rarmure_request_validation`. A master-only `rarmure_promote_candidate` would request a service-authorized promotion. These are proposed names, not existing Harness APIs.

### Identity, authority, and state ownership

Use the runtime caller associated with `exec.agent` and a trusted role/view binding. Do not trust an `agentId` or `role: master` supplied in model-generated arguments. Calls without an authenticated identity must not acquire present authority. The RARMURE service should reject unauthorized operations even if a Harness tool or configuration is incorrectly exposed.

The RARMURE service owns exact project revisions, working views, candidate capture, and master-authorized promotion. SQL would provide durable recording under the chosen design; Qdrant would provide derived retrieval. Workers should receive scoped references through that service rather than unrestricted direct database access.

Harness's session log records what the model saw and the tool/session activity. It is not automatically the RARMURE project revision store. Preserve both responsibilities, link their operation identities, and reconcile interruptions without duplicating effects. Plugin memory is not a durable source of model-visible context. Avoid casually adding new stored Session event types; readers and replay require compatible declarations and formats.

`agent.inject()` queues context for a later step; it does not wake an idle agent or change a request already in progress. Coordination therefore needs explicit message delivery and refresh points before assessing or applying a proposal. Claims that every agent instantly knows a new intention would exceed this mechanism.

## Source-level findings that affect the design

The [tool registry implementation](https://github.com/deepseek-ai/deepseek-harness/blob/5badb15009ae1756c3afe0ae0cef1faafc290ccc/packages/core/tools/src/index.ts) provides `restrict()` on agent-scoped contexts and a synchronous, monotonic `guard()`: a returned denial reason cannot be overridden by another guard. Async policy belongs in the corresponding event pipeline; it does not replace service-side authorization.

The [local filesystem provider](https://github.com/deepseek-ai/deepseek-harness/blob/5badb15009ae1756c3afe0ae0cef1faafc290ccc/packages/fs/fs-local/src/index.ts) explicitly states that `cwd` is a path-resolution default, not containment. The [filesystem service](https://github.com/deepseek-ai/deepseek-harness/blob/5badb15009ae1756c3afe0ae0cef1faafc290ccc/packages/fs/fs/src/index.ts) exposes replaceable resolution, identity, reads, and atomic mutations. Its [opaque file/version types](https://github.com/deepseek-ai/deepseek-harness/blob/5badb15009ae1756c3afe0ae0cef1faafc290ccc/packages/fs/fs/src/types.ts) allow backend-defined IDs and revisions; they are not automatically RARMURE semantic references.

Replacing file tools alone does not confine Bash, terminal commands, generated programs, or trusted Host plugin code. Harness Host plugins execute in-process outside the workspace sandbox. Limit available worker tools, confine spawned processes, isolate service credentials, and make the filesystem and subprocess providers describe the same execution environment. A FUSE-style projection can supply ordinary paths to test tools, but FUSE itself does not supply all process isolation.

The [Agent Teams package](https://github.com/deepseek-ai/deepseek-harness/blob/5badb15009ae1756c3afe0ae0cef1faafc290ccc/packages/experimental/agent-team/README.md) assumes a shared workspace and explicitly does not support separate teammate working directories or cross-process team coordination. Its Lead role is not RARMURE's present-access authority. Its durable messaging may be useful, but it is not a drop-in implementation of candidate-specific execution views or recursive exploration.

## A smaller alternative through MCP

A configuration-only bundle can connect Harness to a RARMURE MCP server over HTTP or stdio, using the existing `@deepseek-ai/dsh-mcp-client`. The repository provides an [MCP bundle template](https://github.com/deepseek-ai/deepseek-harness/blob/5badb15009ae1756c3afe0ae0cef1faafc290ccc/packages/preset/agent-preset/skills/cordis-plugin-development/templates/mcp/cordis.patch.yml).

This could be a small first interface for read, intention, and proposal operations. MCP connectivity alone does not remove local file tools, implement role binding, provide execution isolation, or guarantee context freshness. A native Harness plugin is the appropriate candidate for tighter per-agent policy and lifecycle integration. A public tool endpoint still needs authenticated role/view access.

## Proposed first evaluation

### Parallel workers, provider routes, and review panels

The target integration should dispatch multiple worker sessions against separately authorized virtual working views, then issue fixed candidates to complementary reviewers. An external scheduler would track work-item dependencies, role/view bindings, provider routes, cancellation, budgets, and review rounds. The plugin would translate authorized operations and deliver context at supported agent lifecycle boundaries. RARMURE's service would retain project-state authority.

This is a proposed integration topology, not a verified Harness capability. In particular, per-agent model routing, supported provider interfaces, concurrent session execution, and provider failure recovery need a focused source study and runtime qualification. Native Agent Teams' shared-workspace assumption does not establish the required isolation. Multiple providers must not gain direct database access or present authority.

After the initial keyless checks, a bounded qualification should demonstrate overlapping workers without lost changes, parallel specialist reviews on one fixed candidate, and counter-review of a master selection. Exercise an unavailable provider and stale review: neither may produce an assumed acceptance or unauthorized fallback. Compare elapsed time, resource use, and missed interactions against a sequential baseline before claiming a parallelism benefit.

### Initial adapter checks

Start with a bounded service adapter and two worker views derived from one issued base. Demonstrate authorized reads, intention registration, candidate capture, and stale-base rejection. Verify that workers cannot read or alter the present through tools, retrieval, or subprocesses. Then expose one fixed candidate to an isolated executor, attribute its evidence, and exercise a master-only promotion including a stale or interrupted attempt.

The experiment should also check cancellation, plugin unloading, duplicate event delivery, model-context replay, and an unavailable service. If Team messaging is used, qualify its view-binding limitations explicitly. Use keyless service/mock-model cases before any optional provider-backed exercise. Measure end-to-end outcomes before claiming faster work.

The study supports designing an external plugin first. It does not establish a working RARMURE runtime, and it leaves a Harness fork conditional on a specific extension point proving insufficient.
