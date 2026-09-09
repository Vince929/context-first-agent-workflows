# Case Study Protocol

## Purpose

This protocol helps contributors evaluate whether the workflow reduces navigation and change noise for a real coding task. It is not a universal benchmark and should not be used to manufacture productivity claims.

## Unit of observation

A case study compares one representative task before and after adopting one or more layers of this repository:

- a project map;
- `app + modules + tools` boundaries;
- minimal-context execution protocol.

Use the same task definition where possible. If exact replay is impossible, describe the differences plainly.

## Record these facts

| Field | Description |
| --- | --- |
| Task | A concise user-visible request |
| Repository shape | Language, framework, source-root style, approximate module count |
| Adoption state | Map, structure, execution workflow, or combination |
| Agent and environment | Agent/tool version, editor or CLI, relevant constraints |
| First relevant file | The first implementation file that materially advanced the task |
| Navigation effort | Time, read files, read directories, and search rounds before first edit |
| Change surface | Changed files, changed directories, public-contract changes |
| Validation | What was run, in which environment, and the outcome |
| Clarifications | Number and type of human clarification rounds |
| Limitations | Confounders, missing evidence, and reasons the result may not generalize |

## Suggested measurements

```text
time_to_first_relevant_file
files_read_before_first_edit
directories_read_before_first_edit
search_rounds_before_first_edit
clarification_rounds
files_changed
validation_failures_from_missed_dependencies
```

Use counts as directional evidence, not proof of causal productivity. Report qualitative observations too: did reviewers find the change local, did the map mislead the agent, did a public boundary hide a needed dependency?

## Before/after report template

```markdown
# <Case title>

## Task

<user-visible request>

## Environment

- Stack: <language/framework>
- Agent: <tool/version>
- Adoption state: <map / structure / execution>

## Baseline

- First relevant file: <path>
- Navigation: <time, files, directories, searches>
- Change surface: <files/directories>
- Validation result: <result>

## After adoption

- First relevant file: <path>
- Navigation: <time, files, directories, searches>
- Change surface: <files/directories>
- Validation result: <result>

## Interpretation

<What likely improved, what did not, and why.>

## Limitations

<Confounders and generalization limits.>
```

## Privacy and intellectual property

Do not submit private code, repository identifiers, company names, internal URLs, credentials, logs, or customer data. Replace domain details with synthetic equivalents. If the work was performed under an employment agreement, confirm that sharing a sanitized case study is permitted.
