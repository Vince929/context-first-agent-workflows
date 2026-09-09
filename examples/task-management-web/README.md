# Reference Example: Task Management Web App

This is a synthetic reference example. It contains no production source code, internal paths, credentials, or organization-specific terminology.

## Task

> Add a `priority` filter to the task list and preserve it in the URL query string.

## Before: technology-first layout

```text
src/
  components/
    FilterPanel.tsx
    TaskTable.tsx
  pages/
    TaskListPage.tsx
  services/
    taskService.ts
  models/
    task.ts
  store/
    taskSlice.ts
  utils/
    query.ts
```

An agent receiving the task must infer whether to begin with `pages`, `components`, `services`, `store`, or `utils`. The files are all plausible, but their common business ownership is not visible from the path.

## After: business module layout

```text
src/
  app/
    platform/http/
    routes/
    ui/
  modules/
    task-management/
      pages/TaskListPage.tsx
      components/TaskFilterPanel.tsx
      components/TaskTable.tsx
      api/taskApi.ts
      state/taskListState.ts
      domain/taskQuery.ts
      model/task.ts
  tools/
    maintenance/
```

Now the request maps directly to `src/modules/task-management/`. The agent can read the page, filter component, query rule, state, and API adapter as a local group. It only reaches `app` if URL routing or the HTTP platform behavior is relevant.

## Example project map

```markdown
# Task Management Web Project Map

> A React web application for reviewing and assigning operational tasks.

## Module navigation

| Path | Responsibility | Main entry point / key dependency |
| --- | --- | --- |
| `src/app/routes/` | Route composition and access guards | `AppRoutes.tsx` |
| `src/modules/task-management/` | Task list, filters, assignment, and review flow | `pages/TaskListPage.tsx` |
| `src/app/platform/http/` | Shared HTTP client and request error normalization | `client.ts` |
| `tools/maintenance/` | Offline repair commands | `backfill-task-state.ts` |

## Primary request / data paths

1. `browser entry -> app routes -> task-management page -> task API -> backend`
```

## Expected context-first execution

```text
1. Read PROJECT-MAP.md once.
2. Enter modules/task-management.
3. Read TaskListPage, TaskFilterPanel, taskQuery, taskListState, and taskApi only as needed.
4. Confirm whether URL routing is module-local or app-level.
5. Make the smallest compatible filter/query change.
6. Hand URL persistence validation to the target browser environment.
```

## What this example does not prove

This tree is illustrative. It does not demonstrate a measured speedup. Use the [case study protocol](../../benchmarks/task-protocol.md) on a real, sanitized repository to report evidence.
