# Skills

Each directory contains a standalone `SKILL.md`. The skills are written in a broadly compatible Markdown format and can be adapted to any coding-agent platform.

| Skill | Use it when | Outcome |
| --- | --- | --- |
| [`fast-ai`](fast-ai/SKILL.md) | Any project-related task, to auto-select the right pack skill from one default entry point | A single routing decision that dispatches to the matched skill |
| [`context-first-code`](context-first-code/SKILL.md) | A local implementation, diagnosis, or well-scoped change is requested | Minimal necessary context, minimal correct diff, explicit validation handoff |
| [`project-map`](project-map/SKILL.md) | A user explicitly asks to create or update a project map | A compact root `PROJECT-MAP.md` for cold-start navigation |
| [`ai-friendly-refactor`](ai-friendly-refactor/SKILL.md) | A module migration, directory redesign, codebase restructuring, or large file split is requested | A human-approved migration to `app + modules + tools` boundaries |
| [`human-readable-doc`](human-readable-doc/SKILL.md) | A technical design, research report, conclusion, incident review, migration, or release document is requested | A traceable human-readable Markdown document with a chapter-one table and Mermaid overview diagram |

## Installation

Copy one or all folders into the location your agent discovers skills from. Claude Code-compatible repositories usually use:

```bash
mkdir -p .claude/skills
cp -R skills/* .claude/skills/
```

For other agents, preserve each folder and its `SKILL.md`; adjust only discovery paths or platform-specific metadata when necessary.

## Skill selection

```text
Is the request project-related and should the agent pick the skill automatically?
  -> fast-ai (route first, then run the matched skill)

Is the requested change local and behaviorally clear?
  -> context-first-code

Does the user explicitly request a compact project navigation map?
  -> project-map

Does the request move files, change module boundaries, reorganize directories,
remove shared technical layers, or split large business files?
  -> ai-friendly-refactor

Does the request create or revise a technical design, research report, conclusion,
incident review, migration, release, or other reviewable Markdown document?
  -> human-readable-doc
```

Do not use `project-map` as a substitute for real structural work. Do not use `context-first-code` to silently perform architectural migration.
