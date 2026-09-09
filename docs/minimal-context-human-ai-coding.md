# Minimal-Context Human-Agent Coding

## Thesis

High-throughput agentic coding is not maximized by giving an agent unlimited autonomy. It is improved by assigning uncertainty to the party that can resolve it: people decide goals, compatibility, and acceptance; agents execute deterministic work with the minimum facts needed to do so safely.

## The collaboration boundary

Humans decide:

- desired behavior, success criteria, priorities, and risk tolerance;
- business ownership, architecture boundaries, and compatibility choices;
- release readiness and target-environment acceptance.

Agents execute:

- target and direct-dependency discovery;
- incremental implementation and deterministic batch edits;
- targeted repair from real errors and logs;
- concise change, impact, and validation handoff.

When code and request do not determine a business choice, the agent should ask a focused question rather than manufacture a decision.

## Minimal context

Read facts in descending value:

```text
confirmed goal and constraints
  -> named file or business module
  -> target symbol or endpoint
  -> direct callers and dependencies
  -> required types, configuration, and real failure evidence
```

Avoid treating full-repository scans, broad history reading, all tests, all configuration, or build artifacts as default preparation. Extra context can introduce stale or similar-but-unrelated implementations into the reasoning path.

## Minimal correct diff

For local, behaviorally clear work:

- reuse existing patterns and installed dependencies;
- change only target code and necessary contracts, callers, or configuration;
- avoid opportunistic cleanup, speculative abstractions, future options, and unrelated renaming;
- preserve public behavior unless change is explicitly approved.

If the task moves boundaries, changes public contracts, performs broad import migration, or requires a debatable architecture choice, it is no longer local work. Switch to a planned refactor.

## Real validation

A build or unit test is useful evidence, but it may not represent real credentials, devices, data, permissions, networks, or deployment configuration. Do not run every possible command merely to create a green status. State what was and was not validated.

A productive feedback loop is:

```text
agent makes a local change
  -> human runs it in the target environment
  -> human supplies the original error or failure evidence
  -> agent reads the smallest relevant context and repairs it
  -> human validates again
```

Never weaken checks, skip hooks, hard-code secrets, or alter unrelated configuration simply to make validation appear successful.

## Two modes

| Mode | Use for | Agent behavior |
| --- | --- | --- |
| Context-first execution | Local additions, direct fixes, deterministic edits | Read direct context, make minimal diff, hand off validation |
| Planned refactor | Module moves, directory redesign, broad splitting, contract changes | Analyze facts, propose plan, wait for approval, migrate consistently |

This distinction keeps routine delivery fast while preserving human control over high-impact architectural decisions.
