# The Context-First Methodology

> Reduce the context tax so coding agents reach correct changes faster.

## The problem: context tax before correct changes

Coding agents can generate code quickly. In existing repositories, they often lose time and accuracy before they can generate the *right* change. They must infer where a request belongs, which files form the active path, which implementation is current, and which commands represent real validation.

We call this pre-generation overhead the **context tax**. Broad search may eventually find code, but it also introduces unrelated modules, stale paths, tests, generated output, and similar names into the working context. The result is slower time-to-correct-change, larger change surfaces, and avoidable repair loops.

This project treats reducing that tax as three connected engineering problems:

```text
Structure: can a business request map directly to local code?
Navigation: can an agent choose the first relevant files without scanning everything?
Execution: can a person and an agent divide uncertain decisions from deterministic implementation?
```

## The three layers

### 1. Structure: `app + modules + tools`

The existing source root contains two runtime roles:

```text
<source-root>/app/        application composition and non-business platform capabilities
<source-root>/modules/    business capability vertical slices
tools/                    non-runtime engineering operations
```

A source root remains framework-specific. The architectural rule begins after entering it.

`modules/<capability>` keeps a business request's UI/API, state, rules, models, and private utilities close together. `app` owns startup, routes, platform facilities, global UI, and other non-business capabilities. `tools` keeps migration and operational code out of the runtime path.

### 2. Navigation: `PROJECT-MAP.md`

A compact project map is a semantic index for an unfamiliar repository. It records the application shape, actual entry points, stable modules, high-value platform dependencies, and one to three primary data paths. It is intentionally not a complete inventory.

The map answers: *where should an agent start reading?* The source code answers: *what is true?*

### 3. Execution: minimal context and minimal correct diffs

A human supplies goals, acceptance criteria, compatibility decisions, and real-environment evidence. An agent reads the target and direct dependencies, implements the smallest correct change, and hands target-environment validation back explicitly.

Small implementation work should not silently become architecture work. When boundaries, directories, public contracts, or many imports must change, the workflow changes to analysis, a reviewable plan, explicit approval, and then execution.

## How this improves time-to-correct-change

Agents commonly use three retrieval paths:

1. **Path inference.** A business word such as “recordings” or “billing” should lead to `modules/recordings` or `modules/billing` rather than force a guess between global `components`, `services`, and `models`.
2. **Symbol and import tracing.** Small public module boundaries and one-way dependencies produce shorter, more predictable call chains.
3. **Semantic retrieval.** When a hit is inside a business module, adjacent files are more likely to complete the relevant local context.

The methodology does not claim that a directory name makes an agent correct, or that it makes models emit tokens faster. It aims to improve time-to-correct-change by reducing avoidable search branches, unnecessary context expansion, unrelated edits, and repair loops; the remaining reasoning becomes more local and inspectable.

## Guardrails

- `app` is not a renamed `shared` directory.
- Do not extract business code merely because two modules look similar.
- Do not create empty layers to satisfy a diagram.
- Do not retain compatibility layers for hypothetical callers.
- Do not call local test success a substitute for the target environment.
- Do not ask an agent to make product or compatibility decisions that have not been supplied.

## Adoption order

1. Create a short, accurate `PROJECT-MAP.md`.
2. Apply the execution workflow to new local work.
3. Identify one high-value module for a planned structural migration.
4. Measure navigation, time-to-correct-change, repair loops, and validation outcomes before expanding the convention.

See the detailed papers for [structure](ai-friendly-code-organization.md), [navigation](project-map-and-ai-codebase-mental-model.md), and [execution](minimal-context-human-ai-coding.md).
