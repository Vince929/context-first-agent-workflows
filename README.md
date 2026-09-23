# Context-First

> Faster correct code changes for coding agents.

`Context-First Agent Workflows` is a tool-agnostic skill pack and methodology for improving **time-to-correct-change** in existing repositories.

Coding agents are already fast at generating code. In existing repositories, they are often slow at generating the *right* change. Before an agent writes code, it pays a **context tax**: finding the business module that owns a request, tracing the active path, excluding similar but irrelevant code, and determining what must be validated.

Context-First reduces that context tax through three connected layers:

1. **Structure** — `app + modules + tools` keeps business context local.
2. **Navigation** — `PROJECT-MAP.md` provides a compact cold-start index.
3. **Execution** — humans make decisions while agents implement minimal, evidence-driven changes.

The goal is not to make models emit tokens faster. It is to help agents read **less irrelevant code**, make smaller correct changes, and reach real-environment validation with fewer avoidable search and repair loops.

## The model

```text
User goal
  -> PROJECT-MAP.md selects an entry point and business module
  -> app + modules + tools bounds the local code context
  -> minimal-context execution produces the smallest correct change
  -> real environment validation supplies evidence for the next iteration
```

| Layer | Artifact | Acceleration target |
| --- | --- | --- |
| Structure | `skills/ai-friendly-refactor/` | Reduce long-term context search cost by keeping a business request local. |
| Navigation | `skills/project-map/` | Reduce cold-start time before an agent finds the first relevant files. |
| Execution | `skills/context-first-code/` | Reduce unnecessary changes and repair loops after context is found. |

## Quick start

1. Copy the skills into the skill directory used by your coding agent. For Claude Code-compatible projects:

```bash
mkdir -p .claude/skills
cp -R skills/* .claude/skills/
```

2. Ask your agent to invoke `project-map` explicitly to create `PROJECT-MAP.md`. For example:

```text
Use project-map to generate a compact PROJECT-MAP.md for this repository.
```

The skill performs the minimal navigation scan and writes the map. Use `templates/PROJECT-MAP.md` only when you want to draft or curate a map manually.

3. Use the generated map as the first navigation step for project-specific work, and invoke `project-map` again only when high-value navigation facts change.

4. When a repository needs structural work, invoke `ai-friendly-refactor`; it will analyze first, propose a migration plan, and wait for explicit approval before editing implementation files.

5. When creating or revising a technical design, research report, conclusion, incident review, migration, or release document, invoke `human-readable-doc`; it requires the first chapter to contain a summary, Markdown table, and Mermaid overview diagram.

See [Skills](skills/README.md), [adoption guidance](docs/adoption.md), and the [reference example](examples/task-management-web/README.md).

## Human-readable documents

The skill pack also includes `human-readable-doc` for technical designs, research reports, conclusions, incident reviews, migrations, and release documents. It keeps claims reviewable by requiring a table of contents and placing a summary, Markdown table, and Mermaid overview diagram in chapter one; it also distinguishes confirmed facts, conclusions, and open items.

## What this is not

- Not a replacement for tests, code review, or real-environment validation.
- Not a claim that every project must use the same source-root path or module internals.
- Not a generic `shared/`, `common/`, or `utils/` convention.
- Not a request for agents to autonomously redesign systems without human decisions.
- Not a license to invent metrics, causes, capabilities, or conclusions in human-facing documents.

## Repository layout

```text
skills/       Agent-installable workflows
templates/    Copyable starting points
docs/         Method papers and adoption guidance
examples/     Sanitized before/after reference material
benchmarks/   Case-study protocol and reporting template
```

## Evidence and discussion

This project makes design claims that should be tested, not accepted on naming preference. Good evidence includes:

- time-to-first-relevant-file for a representative task;
- files and directories read before the first edit;
- time-to-correct-change, with task and environment limitations stated;
- user clarification rounds and repair loops;
- changed-file count and review surface;
- validation failures caused by missed dependencies;
- qualitative feedback from maintainers and agents.

Use [GitHub Discussions](../../discussions) for design questions and [Issues](../../issues) for concrete defects or compatibility requests. The [benchmark protocol](benchmarks/task-protocol.md) explains how to publish comparable case studies without exposing proprietary code.

## Documentation

- [The three-layer methodology](docs/methodology.md)
- [AI-friendly codebase structure](docs/ai-friendly-code-organization.md)
- [Project maps and codebase mental models](docs/project-map-and-ai-codebase-mental-model.md)
- [Minimal-context human-agent execution](docs/minimal-context-human-ai-coding.md)
- [Adoption guide](docs/adoption.md)

## Contributing

Contributions are welcome, especially sanitized case studies, agent adapters, counterexamples, and corrections to the guidance. Read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request.

## License

Released under the [Apache License 2.0](LICENSE).
