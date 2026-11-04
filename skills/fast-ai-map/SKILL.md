---
name: fast-ai-map
description: Create or incrementally update a concise root PROJECT-MAP.md with module responsibilities, entry points, and key flows. Use only when the user explicitly requests a project map or refresh.
---

# Fast AI Map

Create a navigation index, not a file inventory or architecture review. Run only on explicit request; other skills must not generate or update the map automatically. Source code remains the truth.

## Create or update

- Check the relevant repository's root `PROJECT-MAP.md`. Reuse its current contents if already in context; read it otherwise.
- First creation: inspect only project configuration, source roots, runtime entry points, top-level business modules, and core platform/data paths needed to establish navigation facts.
- Update: inspect the requested change scope and necessary direct files. Change only verified module paths, responsibilities, entry points, or key flows; leave the map untouched if none changed.
- Do not inspect dependencies, build output, caches, version-control metadata, generated files, environment files, logs, or potentially sensitive files. Never include secrets, tokens, private addresses, or environment values.

## Map format

Start with `# <Project name> Project Map` and one sentence describing its purpose and technology/runtime. Then:

1. **Module navigation:** one table with `Path | Responsibility | Main entry point / key dependency`. List key source directories at one or two levels, stable business modules, shared platform capabilities, and important app/worker/CLI/native entry points. Use deeper paths only when needed for navigation.
2. **Primary request / data paths:** one to three verified flows in the form `entry → key processing module → data source or output`; omit this section if it adds no useful navigation information.

Use the module table as the semantic directory outline; do not add a duplicate directory tree. Usually keep the map under 100 lines, shorter for small projects. Include only facts that help choose the next file to read; do not invent responsibilities or flows.

Exclude per-file, class, function, field, and test inventories, technical-debt lists, design debates, and refactoring proposals. No filler or repeated explanations of table rows.

## Delivery

Re-read once for verified paths, accurate responsibilities, and sensitive information. Reply with the map path and one line stating creation, changed facts, or why no update was needed; do not paste the map again.

Do not run build, tests, lint, deployment, or browser validation as part of mapping. State unresolved facts or unperformed checks only when relevant.
