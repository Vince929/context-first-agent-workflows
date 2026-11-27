---
name: fast-ai
description: Routes project-related work to fast-ai-code, fast-ai-refactor, fast-ai-map, or fast-ai-doc and runs the selected skill. Use for implementation, debugging, clarifying or answering questions about a project, reading code, refactoring, migrations, explicit project map requests, or technical writing. Do not use for general knowledge questions or unrelated conversation.
---

# Fast AI Router

Classify the task and hand it off to the selected skill. Do not implement, refactor, or write documentation here; the selected skill defines how to do the work and verify it.

> Keep the router and all four `fast-ai-*` skills in sibling directories under the same skill discovery directory. Use the same identifiers for source directories, `SKILL.md` names, installation directories, and routing.

## Route the task

1. Honor any skill or mode the user explicitly requests. Answer general knowledge questions and unrelated conversation without using this router.
2. Otherwise, choose a skill by the **primary deliverable** in the table below.
3. **Follow the selected skill's boundaries, output, and handoff rules.** If its instructions are not already in context, load them immediately using the host's skill mechanism, or read its `SKILL.md` if none is available. Reuse instructions already in context across turns and tasks.
4. Reuse the router and task skills by actual file path; copies with the same name are not interchangeable. Reload only if the file changed, context compaction removed instructions you need, or the user requests a refresh. Load only what is missing or changed. Do not check timestamps, list directories, or report what was loaded on every turn.

| Primary deliverable or task | Route to |
| --- | --- |
| Implement or modify project code, locate or diagnose an issue, clarify project behavior, read code, or make a targeted fix based on an actual error | `fast-ai-code` |
| Migrate modules, reorganize directories or module boundaries, split files or remove duplication as the main task, or change the architecture | `fast-ai-refactor` |
| Create or update a project map or `PROJECT-MAP.md` at the user's explicit request | `fast-ai-map` |
| Write or revise reviewable Markdown for a technical design, architecture, API, research, conclusions, incident review, migration plan, or release plan | `fast-ai-doc` |

## Precedence and exceptions

- For changes to module boundaries or cross-module contracts, or for moving many files, use `fast-ai-refactor`. Produce a plan and wait for approval before editing. Complexity alone does not make a task a refactor.
- For an explicitly requested, localized change to a public contract that does not meet those refactoring criteria, use `fast-ai-code` and check direct callers and compatibility impact.
- If an oversized business file needs a small split along responsibility lines as part of the requested implementation, use `fast-ai-code`. If the task itself is to reorganize directories or boundaries, use `fast-ai-refactor`.
- Create or update a project map only on explicit request, never as a side effect of coding.
- Choose one primary skill. If the task includes both code and documentation, start with the primary deliverable. When multiple skills are necessary, load them in sequence and state the order. For refactors, plan first; documentation usually follows once the implementation is settled.

## Default invocation prompt

Add this prompt to the agent's global or project rules:

```text
Default workflow: For project-related tasks, use fast-ai to select the appropriate skill and follow it. Reuse the router and skill instructions if they are already in context; otherwise, load them first.
If I specify another skill or mode, follow my request instead. Do not use fast-ai for general knowledge questions or unrelated conversation.
```
