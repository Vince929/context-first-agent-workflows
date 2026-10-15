# Adoption Guide

## Start with one real repository

Do not begin by moving every folder. Select a repository and one recurring task class where agents currently lose time: finding the right module, understanding a request path, or making a small change without unrelated churn.

## Step 1: install the skills

Copy the five sibling folders (`fast-ai`, `fast-ai-code`, `fast-ai-refactor`, `fast-ai-map`, and `fast-ai-doc`) to the discovery directory used by the selected coding agent. Preserve folder names, frontmatter `name` values, and the flat layout. Use `fast-ai` as the default entry point to route project-related tasks, or invoke a task skill directly. When upgrading, remove old-name skill directories and any child skill copies nested inside the installed `fast-ai/` directory to avoid duplicate discovery. See the [installation instructions](../skills/README.md#installation).

## Step 2: create the project map

Explicitly invoke `fast-ai-map` to create a root `PROJECT-MAP.md`. Review it with maintainers. The first version should be concise enough to read before a task, and accurate enough to select the next files.

## Step 3: use context-first execution for normal work

For a few weeks, use `fast-ai-code` for local implementation and real-error repair. Record where its assumptions fail: missing maps, unclear module ownership, ambiguous contracts, or validation gaps.

## Step 4: choose one structural migration

When a real pain point demonstrates that code is scattered, invoke `fast-ai-refactor` for one module or boundary. Require a plan before edits. Do not convert the whole repository because a target diagram looks attractive.

## Step 5: measure and publish learning

Use the [case-study protocol](../benchmarks/task-protocol.md). Compare similar tasks before and after adoption, but do not invent productivity claims. Include counterexamples and failure modes.

## Recommended initial metrics

- Time from task receipt to first relevant implementation file.
- Files and directories read before the first edit.
- User clarification rounds.
- Files changed per completed task.
- Validation failures caused by an omitted direct dependency.
- Reviewer feedback about change locality and readability.

## Questions to settle locally

- What counts as a stable business module in this product?
- Which imports are permitted across module boundaries?
- Which platform capabilities belong in `app`?
- What target-environment checks are mandatory before release?
- Which team member can approve structural migration and compatibility policy?

The skills provide defaults. Repository maintainers own these decisions.
