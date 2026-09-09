# Publishing Checklist

## Before creating a public repository

- [ ] Confirm that your employment agreement and company policy permit publishing the skills, methodology, and examples.
- [ ] Re-read all files for organization names, internal project names, private paths, private URLs, credentials, tokens, logs, screenshots, customer data, and proprietary code.
- [ ] Replace generic license attribution in `LICENSE` only if a legal or organizational policy requires a copyright notice.
- [ ] Decide the repository owner, public name, description, and primary discussion language.
- [ ] Confirm whether Apache License 2.0 is appropriate for both skills and documentation in your jurisdiction and organization.

## Create the remote repository

Suggested settings:

- Name: `context-first-agent-workflows`
- Description: `Reduce the context tax so coding agents reach correct changes faster.`
- Visibility: Public, only after the pre-publication review is complete.
- License: Apache-2.0.
- Features: enable Issues and Discussions.
- Topics: `coding-agents`, `agent-skills`, `claude-code`, `context-engineering`, `ai-assisted-development`, `software-architecture`, `vertical-slice-architecture`.

## First release

1. Push this local repository.
2. Open Discussions using the category plan in `.github/DISCUSSION_TEMPLATE.md`.
3. Create a `v0.1.0` release that identifies the three skills as an experimental methodology, not a proven universal standard.
4. Publish a short announcement that leads with the problem: agents generate code quickly but lose time reaching the correct change because of context tax in existing repositories.
5. Link the reference example and ask for counterexamples, agent adapters, and sanitized case studies.

## Suggested launch post

```text
I am publishing an experimental workflow for coding agents in existing repositories.

Coding agents are fast at generating code, but often slow at reaching the correct change. Before generation, they pay a context tax: finding the owning business module, tracing the active path, excluding irrelevant code, and determining what must be validated.

Context-First aims to reduce that tax through three layers:
- app + modules + tools for local business context;
- PROJECT-MAP.md for cold-start navigation;
- minimal-context execution where humans make decisions and agents make the smallest evidence-driven change.

I am looking for counterexamples and sanitized case studies, especially across Python, Java/Kotlin, Go, Rust, and frontend monorepos.
```

## Do not claim yet

Do not claim a percentage token reduction, speedup, or defect reduction until a reproducible case study provides the underlying measurements and limitations. State the intended effect instead: reduce context tax and improve time-to-correct-change by reducing unnecessary context expansion, time-to-first-relevant-file, unrelated edits, and repair loops.
