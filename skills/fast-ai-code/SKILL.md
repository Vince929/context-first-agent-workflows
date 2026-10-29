---
name: fast-ai-code
description: Execute well-scoped coding work with minimal necessary context, minimal correct diffs, and explicit real-environment validation handoff. Use for project-specific implementation, diagnosis, clarification, and fixes that do not require architectural migration.
---

# Fast AI Code

Read only the facts that can change the implementation decision, then make the smallest correct change.

## Decision boundary

Humans decide business goals, acceptance criteria, priorities, risk tolerance, module ownership, contract and compatibility policy, and release readiness. When a necessary business or compatibility choice cannot be inferred from the request and code, ask only the necessary clarification; do not invent product decisions.

If the work changes module boundaries or cross-module contracts, moves many files, or requires an architectural choice, stop and switch to `fast-ai-refactor` for a plan and explicit approval before implementation edits. A user-approved local external-contract change can stay in this workflow; inspect direct callers and compatibility impact.

## Context protocol

1. Read the root `PROJECT-MAP.md` once if it exists and has not already been loaded in the current task. Use it only to choose where to start; source code remains the implementation truth. Do not generate or update the map unless explicitly requested.
2. Read in order: user goal and constraints → named file or matching business module → target component/function/endpoint → direct callers and dependencies → required types, configuration, and real error evidence.
3. Expand context only when a missing fact blocks a correct implementation. Do not routinely scan the full repository, list broad directories, read all tests, or inspect build artifacts and history.

## Minimal correct diff

Default to the smallest change that satisfies the confirmed request:

- reuse project conventions, standard libraries, and installed dependencies;
- edit only the target implementation plus required contracts, callers, or configuration;
- preserve public behavior and external contracts unless the user explicitly approves a change;
- do not add speculative abstractions, one-implementation interfaces, future configuration, unrelated cleanup, or new dependencies without need;
- keep business-private code inside its owning module;
- if a business source file becomes too large during the requested work, split only along clear responsibility boundaries and preserve its public behavior.

## Validation boundary

Do not run build, tests, lint, formatting, services, or simulation loops by default. A local green result does not replace target-environment validation with real credentials, devices, data, permissions, network dependencies, or deployment configuration.

- Re-read the edited area once.
- When the user supplies a real build, runtime, or test failure, read the smallest necessary context and make a targeted repair.
- Never bypass hooks, weaken checks, hard-code secrets, or modify unrelated configuration merely to make validation appear successful.

## Completion response

Keep the final response concise:

- changed behavior and key files;
- contract or compatibility impact, if any;
- what to validate in the target environment and which checks actually ran; if none ran, state that no build, test, or lint was run.

## Examples

- “Add a required field to the existing form.” → Read the form, its submit contract, direct consumer, and relevant type; make the smallest compatible change.
- “Move all order code into a new module.” → Do not start editing; use `fast-ai-refactor` and produce a plan first.
