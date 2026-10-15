---
name: fast-ai-refactor
description: Refactor an existing project toward app + modules + tools boundaries so coding agents can locate business context quickly. Analyze first, produce a reviewable migration plan, and wait for explicit human approval before implementation edits.
---

# Fast AI Refactor

## Purpose

Improve codebase navigability and change safety by organizing runtime source around two roles inside the existing source root:

```text
<source-root>/
  app/                    # application composition and non-business platform capabilities
  modules/                # business capability vertical slices
tools/                    # non-runtime engineering operations
```

`<source-root>` remains framework-specific: it may be `src/`, `src/<package>`, `src/main/<language>`, or an existing language package root. The method standardizes the first architectural decision after entering source code; it does not force identical physical paths across ecosystems.

The objective is to keep a business request's primary page/API, state, rules, model, and private utilities near one another. It is not a justification for a whole-repository rewrite, empty folders, or speculative abstraction.

## Structural rules

### Modules

A module is a user-recognizable business capability:

```text
modules/<capability>/
```

Name modules with business language, not technical categories, database tables, or team ownership. Keep module-private UI, API, state, domain logic, models, validation, persistence adapters, and tests inside the owning module.

Module internals are technology-specific and only include necessary layers:

```text
# frontend example
pages/ components/ api/ state/ domain/ model/

# backend example
api/ application/ domain/ infrastructure/ models/ schemas/
```

### App

`app/` explains how the whole application runs. It may contain `bootstrap`, `routes`, `layout`, `state`, `platform`, `ui`, `i18n`, `lib`, `types`, and `styles` when those capabilities actually exist.

A file belongs in `app` only when it is non-business-specific, serves the application or several stable modules, and has a precise capability name. `app` is not a renamed `shared` directory.

Do not retain top-level `shared`, `common`, `utils`, `components`, `services`, or `models` as default destinations for business code. Use this order instead:

1. business-specific code -> owning `modules/<capability>/`;
2. stable, cross-module, non-business capability -> precise `app` subdirectory;
3. offline migration, maintenance, operations, or generation -> `tools/`;
4. uncertain ownership -> keep it in the current owning module.

### Tools

Keep non-runtime engineering operations outside the source root, organized by intent when useful: `migration`, `maintenance`, `operations`, or `generation`. Tools must not become hidden runtime dependencies or bundled application code.

### Dependencies

```text
modules/* -> app/*
app/platform, app/ui, app/lib, app/types -> no dependency on concrete modules/*
app/bootstrap, app/routes -> may compose modules/*
module A -> no deep imports of module B private implementation
tools/* -> not part of runtime application output
```

Modules collaborate through small public boundaries such as an explicit contract, route definition, application service, or event. Do not introduce broad barrel exports merely for convenience.

## Scope modes

- **Local refactor (default):** inspect only the user-named module/directory and direct dependencies. Do not run validation commands; hand off minimal validation steps.
- **Whole-project AI-friendly refactor:** only when the user explicitly requests whole-project restructuring or migration to `app + modules + tools`. Inspect implementation source and required project configuration while excluding tests, build configuration, generated code, dependencies, artifacts, caches, and environment files from the structural scan. Run one standard build and one full test command after approved implementation, collecting results without iterative repair.

## Workflow

### 1. Analyze facts

Identify the actual source root, build constraints, entry points, business capabilities, platform capabilities, offline tools, cross-module dependencies, external contracts, and business source files above 500 lines.

Use user-recognizable capabilities to define module boundaries. Do not infer boundaries mechanically from current technical folders, database tables, or API prefixes.

### 2. Plan and obtain approval

Before creating, moving, deleting, or editing implementation files, provide a concise plan containing:

- source root and target `app + modules + tools` tree;
- module responsibilities and internal layers;
- files to create, move, split, merge, or delete;
- classification of existing shared/global technical code and its destination rationale;
- public module boundaries, dependency direction, and repository-wide import migration;
- old entry-point removal and only explicitly approved compatibility layers;
- external-contract impact, treatment of files over 500 lines, risks, and decisions requiring human input.

Wait for explicit approval. If new information would change the approved boundary or compatibility policy, stop and request renewed approval.

### 3. Implement and deliver

After approval, migrate all in-repository imports, remove obsolete paths and unapproved compatibility layers, and preserve behavior and public contracts unless the approved plan says otherwise.

Do not retain a compatibility layer for hypothetical external callers. Retain one only when an external dependency is confirmed and the user explicitly requests it; document its scope, removal condition, and risk.

For local refactors, do not run build, tests, lint, or formatting. For whole-project mode, identify the standard build and full-test commands from project scripts, config, or CI; run each once, collect raw results, and do not iterate automatically.

## Delivery template

```markdown
## Refactor summary

- Source root and runtime roles: <source root; app/modules/tools boundary>
- Business modules: <responsibilities and file operations>
- Application platform: <what moved into app and why>
- Engineering tools: <what moved into tools>
- Imports and compatibility: <repository migration and public behavior>
- Compatibility inventory: <approved retained layers, or none>
- Validation handoff: <local minimal validation, or whole-project results>
- Commit: <result when applicable>
```
