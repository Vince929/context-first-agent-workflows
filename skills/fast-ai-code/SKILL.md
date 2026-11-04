---
name: fast-ai-code
description: Execute well-scoped coding work with minimal necessary context, the smallest complete change, and explicit real-environment validation handoff. Use for project-specific implementation, diagnosis, clarification, and fixes that do not require architectural migration.
license: Apache-2.0 AND MIT
---

# Fast AI Code

Read only the facts that can change the implementation decision. Solve the whole problem with the least new code: be lazy about the solution, never about completing the change.

## Decision boundary

Humans decide business goals, acceptance criteria, priorities, risk tolerance, module ownership, contract and compatibility policy, and release readiness. When a necessary business or compatibility choice cannot be inferred from the request and code, ask only the necessary clarification; do not invent product decisions or omit explicit requirements.

If the work changes module boundaries or cross-module contracts, moves many files, or requires an architectural choice, stop and switch to `fast-ai-refactor` for a plan and explicit approval before implementation edits. A user-approved local external-contract change can stay in this workflow; inspect callers and compatibility impact. Otherwise preserve public behavior and contracts.

Commit only when the user explicitly requests it.

## Context and scope

1. If the user names a file or the target is clear, read the target directly. Otherwise use the relevant repository's root `PROJECT-MAP.md` if it exists. Reuse navigation already present in the current conversation, including injected context; do not re-read it for each message or task. Reload only if the map changed, required content is unavailable after context compaction, or the user requests a refresh; read only needed sections. Do not check timestamps or look for the map every turn. A different repository needs its own navigation, only when location is unclear. The map guides navigation; source code remains the truth. Do not generate or update the map unless explicitly requested.
2. Read in order: user goal and constraints → named file or matching business module → target component/function/endpoint → callers and dependencies → required types, configuration, and real error evidence.
3. Before editing, identify every place the change must reach: callers, tests, fixtures, configuration, and exports. Check what could break for users, including data loss, data exposure, and incompatible callers. That is scope; extra features are not.
4. Expand context only when a missing fact blocks a correct implementation, including tracing affected callers beyond the first hop. Do not routinely scan the full repository, list broad directories, read all tests, or inspect build artifacts and history. For a bug fix, search every caller of the function being changed and fix the root cause once in shared code.

## The smallest complete change

After understanding the scope, take the first option that fully works:

1. **Does it need to exist?** Skip features, options, and flexibility nobody asked for. A vague request gets the smallest version that does the core job, without inventing business decisions.
2. **Already in this codebase?** Reuse the helper, component, service, or pattern the way the surrounding code does.
3. **Standard library or platform feature?** Use it, unless the project has its own. A house component beats a native widget.
4. **An installed dependency?** Use it. Never add a dependency for a few lines.
5. **One line a reader understands at a glance?** One line. A one-liner that needs decoding is not short.
6. **Otherwise:** the minimum code that fully works.

- Finish every part the task needs, including callers, tests, and fixtures the change breaks. The shortest working diff wins only after its full scope is known.
- No unrequested abstraction, wrapper, type conversion, option, configuration, boilerplate, unrelated cleanup, or code "for later". Keep values in the form the platform provides; deletion beats addition.
- Keep the existing layers, interfaces, and conventions; business-private code stays in its owning module. If a business source file becomes too large during the requested work, split only along clear responsibility boundaries and preserve public behavior.
- Code you move or merge keeps its error handling and validation. Between options of equal size, choose the one that is correct on edge cases.
- Comment only the why the code cannot show, in one line. A shortcut with a known limit gets `shortcut: <the limit>, <when to upgrade>`.
- Never cut trust-boundary validation, data-loss prevention, security, accessibility, real-hardware calibration, or anything the user explicitly requested.

## Checks and validation

- New non-trivial logic (a branch, loop, parser, money or security path, or a whole new script or app) leaves one small test or assert-based self-check. Reuse existing test conventions and extend a relevant test when possible; do not introduce a framework or a broad suite. Trivial changes need no new test.
- Leaving a runnable check is not the same as executing it. Do not run build, tests, lint, formatting, services, or simulation loops by default; run relevant checks when the user requests validation. A local green result does not replace target-environment validation with real credentials, devices, data, permissions, network dependencies, or deployment configuration.
- Re-read the edited area once. When the user supplies a real build, runtime, or test failure, read the smallest necessary context and make a targeted repair.
- Never bypass hooks, weaken checks, hard-code secrets, or modify unrelated configuration merely to make validation appear successful.

## Completion response

State the changed behavior and key files, plus contract or compatibility impact when relevant. Do not repeat code already applied or narrate routine steps; provide explanations when requested.

End with one or two short lines: what was skipped or not checked, what to validate in the target environment, and any risk the user must know. Report only checks actually run; if none ran, state that no build, test, or lint was run.

## Examples

- “Add a required field to the existing form.” → Read the form, submit contract, consumers, and relevant types; update affected validation and tests without replacing the project's form component.
- “This shared function crashes for an empty input.” → Search all callers, fix the root cause in the shared function, and extend one relevant regression test; do not add a guard at each caller or run the whole suite by default.
- “Move all order code into a new module.” → Do not start editing; use `fast-ai-refactor` and produce a plan first.

Core change-selection and safety rules adapted from [Ponytail v5.3.3](https://github.com/DietrichGebert/ponytail), Copyright (c) 2026 DietrichGebert, under MIT; see [LICENSE](LICENSE). Context, decision, and validation boundaries follow this repository's Apache-2.0 workflow.
