# AI-Friendly Code Organization

## Thesis

A codebase is easier for coding agents to change when a business request maps to a bounded physical area of code. The recommended target is not a universal folder tree; it is a role model:

```text
<source-root>/
  app/        application composition and non-business platform capabilities
  modules/    business capability vertical slices
tools/        non-runtime engineering operations
```

The existing language and framework decide `<source-root>`. React may use `src/`; Python may use `src/<package>/`; Java and Kotlin may use `src/main/<language>/`. Do not trade ecosystem conventions for visual uniformity.

## Modules: business language first

A module is named for a user-recognizable capability, not a technical category:

```text
modules/
  task-management/
  collection-site/
  recordings/
  identity/
```

Within a module, use only layers that the stack and capability need. A frontend module may contain `pages`, `components`, `api`, `state`, `domain`, and `model`. A backend module may contain `api`, `application`, `domain`, and `infrastructure`.

The key rule is locality: code that exists mainly to implement one capability remains in that capability. This includes UI, request handlers, state, types, validation, domain rules, persistence adapters, and private utilities.

## App: composition, not a dumping ground

`app/` can include concrete horizontal capabilities such as:

```text
bootstrap/ routes/ layout/ state/ platform/ ui/ i18n/ lib/ types/ styles/
```

A capability belongs in `app` only when it is non-business-specific, serves the whole application or several stable modules, and has an explicit name. `platform/http` conveys meaning; `shared` does not.

Do not move domain concepts into `app` because more than one module reads them. The module that owns the concept should expose a small contract, service, route definition, or event boundary instead.

## Tools: separate operational intent

Keep scripts that are not application runtime behavior at the repository root:

```text
tools/
  migration/
  maintenance/
  operations/
  generation/
```

This helps agents distinguish online request paths from offline repair and release operations.

## Dependency direction

```text
modules/* -> app/*
app/platform, app/ui, app/lib, app/types -> no concrete module dependencies
app/bootstrap, app/routes -> may compose modules/*
module A -> no deep import of module B private implementation
tools/* -> no runtime application output
```

Directory names alone do not enforce this. Add import rules, package boundaries, code review checks, or conventions appropriate to the language when the repository is ready.

## A practical extraction rule

Do not use a global shared layer as a default. Use this classification order:

1. one business owner -> its module;
2. stable cross-module use with no business meaning -> an explicit `app` capability;
3. migration or operational intent -> `tools`;
4. uncertain ownership -> keep the code near its current business owner.

A third stable caller is often a useful point to reconsider extraction, but it is not a mathematical rule. Preserve local clarity over speculative reuse.

## Migration warning

Moving files changes imports, tooling assumptions, public paths, and sometimes runtime behavior. Structural migration must start with a reviewable plan that lists ownership, file moves, dependency direction, compatibility policy, and validation. Use the `fast-ai-refactor` skill rather than treating this document as permission for an autonomous rewrite.
