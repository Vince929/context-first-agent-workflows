# Skills

Each directory contains a standalone `SKILL.md`. The router and four task skills are sibling directories under `skills/`, not nested inside `fast-ai/`. Directory names, frontmatter `name` values, installed names, and routing references use the same identifiers; the shared `fast-ai` prefix makes the pack easy to filter. The skills are written in a broadly compatible Markdown format and can be adapted to any coding-agent platform.

| Skill | Use it when | Outcome |
| --- | --- | --- |
| [`fast-ai`](fast-ai/SKILL.md) | Any project-related task, to auto-select the right pack skill from one default entry point | A single routing decision that dispatches to the matched skill |
| [`fast-ai-code`](fast-ai-code/SKILL.md) | A local implementation, diagnosis, or well-scoped change is requested | Minimal necessary context, minimal correct diff, explicit validation handoff |
| [`fast-ai-map`](fast-ai-map/SKILL.md) | A user explicitly asks to create or update a project map | A compact root `PROJECT-MAP.md` for cold-start navigation |
| [`fast-ai-refactor`](fast-ai-refactor/SKILL.md) | A module migration, directory redesign, codebase restructuring, or large file split is requested | A human-approved migration to `app + modules + tools` boundaries |
| [`fast-ai-doc`](fast-ai-doc/SKILL.md) | A technical design, research report, conclusion, incident review, migration, or release document is requested | A traceable human-readable Markdown document with a chapter-one table and Mermaid overview diagram |

## Installation

Copy all five folders to use the `fast-ai` router, or copy an individual task skill for standalone use. Run the following from this repository root, replacing `.claude/skills/` with your target project's skill discovery directory if needed:

```bash
mkdir -p .claude/skills
cp -R skills/fast-ai skills/fast-ai-* .claude/skills/
```

For other agents, preserve each folder name, its `SKILL.md`, and the flat sibling layout; adjust only discovery paths or platform-specific metadata when necessary. When upgrading, remove the old `context-first-code`, `ai-friendly-refactor`, `project-map`, and `human-readable-doc` skill directories, including copies nested inside the installed `fast-ai/` directory, to avoid duplicate discovery.

## Skill selection

```text
Is the request project-related and should the agent pick the skill automatically?
  -> fast-ai (route first, then run the matched skill)

Is the requested change local and behaviorally clear?
  -> fast-ai-code

Does the user explicitly request a compact project navigation map?
  -> fast-ai-map

Does the request move files, change module boundaries, reorganize directories,
remove shared technical layers, or split large business files?
  -> fast-ai-refactor

Does the request create or revise a technical design, research report, conclusion,
incident review, migration, release, or other reviewable Markdown document?
  -> fast-ai-doc
```

Do not use `fast-ai-map` as a substitute for real structural work. Do not use `fast-ai-code` to silently perform architectural migration.
