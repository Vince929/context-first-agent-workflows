# Context-First Agent Workflows

> Help coding agents find the right context before they change code.

`Context-First Agent Workflows` is a small, tool-agnostic skill pack and method for working with coding agents in existing repositories. It treats agent productivity as three connected problems:

1. **Structure** — keep the codebase predictable with `app + modules + tools`.
2. **Navigation** — maintain a compact `PROJECT-MAP.md` for cold-start orientation.
3. **Execution** — let humans make decisions while agents implement minimal, evidence-driven changes.

The goal is not to make agents read the whole repository faster. It is to help them read **less irrelevant code**, make smaller changes, and hand validation back to the environment that can provide real evidence.

## The model

```text
User goal
  -> PROJECT-MAP.md selects an entry point and business module
  -> app + modules + tools bounds the local code context
  -> minimal-context execution produces the smallest correct change
  -> real environment validation supplies evidence for the next iteration
```

| Layer | Artifact | Main question it answers |
| --- | --- | --- |
| Structure | `skills/ai-friendly-refactor/` | Where should code live so a business request has local context? |
| Navigation | `skills/project-map/` | Where should an agent start reading an unfamiliar repository? |
| Execution | `skills/context-first-code/` | How should people and agents divide decisions, implementation, and validation? |

## Quick start

1. Copy the skills into the skill directory used by your coding agent. For Claude Code-compatible projects:

```bash
mkdir -p .claude/skills
cp -R skills/* .claude/skills/
```

2. Create a compact project map from the template:

```bash
cp templates/PROJECT-MAP.md ./PROJECT-MAP.md
```

3. Ask your agent to generate or update the map explicitly, then use it as the first navigation step for project-specific work.

4. When a repository needs structural work, invoke `ai-friendly-refactor`; it will analyze first, propose a migration plan, and wait for explicit approval before editing implementation files.

See [Skills](skills/README.md), [adoption guidance](docs/adoption.md), and the [reference example](examples/task-management-web/README.md).

## What this is not

- Not a replacement for tests, code review, or real-environment validation.
- Not a claim that every project must use the same source-root path or module internals.
- Not a generic `shared/`, `common/`, or `utils/` convention.
- Not a request for agents to autonomously redesign systems without human decisions.

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
- number of files and directories read before the first edit;
- number of user clarification rounds;
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
