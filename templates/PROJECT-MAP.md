# <Project name> Project Map

> One sentence: <what this project does + its primary technology or runtime shape>.

## Module navigation

| Path | Responsibility | Main entry point / key dependency |
| --- | --- | --- |
| `<source-root>/app/` | Application startup, composition, and non-business platform capabilities | `<bootstrap or route entry>` |
| `<source-root>/modules/<capability>/` | <user-recognizable business capability> | `<main page, endpoint, service, or state entry>` |
| `tools/` | Non-runtime migration, maintenance, operations, and generation | `<representative command or script>` |

## Primary request / data paths

1. `<runtime entry> -> <application composition> -> <business module> -> <data source or output>`
2. `<optional worker/CLI/event entry> -> <key processing module> -> <output>`

<!--
Keep this map short. Include only facts that help a person or coding agent choose the next files to read.
Do not include per-file inventories, implementation details, secrets, private URLs, environment values,
build products, logs, generated code, or design debates.
-->
