# Project Maps and AI Codebase Mental Models

## A project map is a cold-start index

When an agent first enters a repository, the immediate problem is orientation: what runs here, where is the source root, which modules represent the user-facing capabilities, and what paths carry the most important requests or data.

A root `PROJECT-MAP.md` compresses those facts into a small semantic index. It should help select the next files to read, not replace source code, architecture records, or test suites.

## Minimal map shape

```markdown
# <Project name> Project Map

> One sentence: <project purpose + runtime form>

## Module navigation

| Path | Responsibility | Main entry point / key dependency |
| --- | --- | --- |
| `<path>` | <responsibility> | <entry/upstream/downstream> |

## Primary request / data paths

1. `<entry> -> <processing> -> <data source/output>`
```

Keep the map near 100 lines or fewer. Include actual entry points, stable business modules, shared platform capabilities with broad impact, and one to three representative paths. Exclude file inventories, implementation detail, secrets, private addresses, logs, generated output, and architecture debates.

## Two indexes, two jobs

```text
PROJECT-MAP.md
  -> semantic index: where should reading start?

app + modules + tools
  -> physical index: what code is likely adjacent and relevant after arrival?
```

A map cannot fix a codebase where a business capability is scattered over global technical folders. A well-organized repository still benefits from a map because the agent may not know which module represents the user's language or where the application begins.

## Maintenance model

Generate a map with one minimal scan when it does not exist. Later, update it only when high-value navigation facts change:

- module boundaries are added, merged, split, or removed;
- runtime, worker, CLI, or route entry points change;
- a primary request, data, or event path changes;
- a broadly used platform capability changes ownership.

Do not regenerate it after ordinary component edits, local function changes, test updates, or unrelated build output changes. A map that is short and accurate is useful; a map that is detailed but stale is actively misleading.

## Trust boundary

The map is a navigation hypothesis. Types, implementations, imports, and runtime configuration are still the facts that govern a change. An agent should read the map once to choose scope, then verify the target code directly.
