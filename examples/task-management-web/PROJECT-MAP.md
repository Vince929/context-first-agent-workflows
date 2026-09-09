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
