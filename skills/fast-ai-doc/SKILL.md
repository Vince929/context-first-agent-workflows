---
name: fast-ai-doc
description: Create or revise concise, evidence-backed Markdown for technical designs, architecture, APIs, research, incident reviews, migrations, and release plans. Lead with conclusions; include a table of contents and a chapter-one summary, table, and Mermaid overview. Use short sentences, remove repetition, and never invent facts or commitments.
---

# Fast AI Doc

Write the shortest document that lets a reader understand the conclusion, evidence, impact, and next action. Concise means no filler, not missing facts or risks.

## Evidence and scope

- Read only user-named material and direct dependencies needed for accuracy. Reuse established terms, API names, paths, and facts.
- Distinguish confirmed facts, decisions supported by requirements or evidence, and hypotheses or open items. Do not present a proposal as an implemented capability or infer causation from correlation.
- Do not invent metrics, coverage, performance, costs, dates, causes, capabilities, owners, or commitments. Numbers need a source and relevant conditions or limitations; distinguish targets from measurements.
- Ask only when a missing premise changes the conclusion. Otherwise consolidate unknowns under open items; do not fill gaps with speculation.

## Structure

Follow an explicitly requested format. Otherwise use a table of contents matching the headings, then:

1. **Chapter one:** a brief conclusion or decision summary → one Markdown table → one Mermaid overview diagram, in that order and within the chapter. Cover the subject, affected systems, primary flow, and scope limits. Adapt labels to the document: design decision, research finding, incident conclusion, or implementation plan.
2. **Necessary detail only:** add the background, design or analysis, contracts, trade-offs, evidence, or rollout details needed to explain or execute the conclusion. No fixed chapter count or empty sections.
3. **Risks and next actions:** consolidate uncertainties, prerequisites, and follow-up work. Include observable acceptance criteria when relevant; avoid vague criteria such as "should work."

For an explicitly requested minimal notice, changelog, or alternative format, omit structural elements that do not fit. Do not add sections, tables, or diagrams merely to make the document look substantial.

- Use tables for comparison or structured facts; use prose for the conclusion and diagrams for relationships. Do not restate every table row or diagram node in prose.
- Mermaid nodes and arrows must represent confirmed actions, components, or analysis paths. Keep the overview on the main path; show uncertainty explicitly rather than inventing services or causal links. Use `<br/>` for label line breaks, never literal `\n` or `\\n`.
- Include exact contracts and relevant failure handling, compatibility, security, data-loss risks, validation, or rollback details when the subject requires them. Describe sequence only where a real dependency exists.

## Concise writing

- Lead each section with its answer or decision. Use direct verbs and short sentences; one main point per sentence or bullet. Split dense sentences without turning them into fragments.
- Delete throat-clearing, slogans, stock transitions, redundant adjectives, and unsupported praise such as "comprehensive," "robust," or "seamless." Replace "in order to" with "to" and "it is important to note that" with the fact itself.
- State each fact once in its proper place. The opening summary may name key conclusions; later sections add evidence or detail, not paraphrases of the summary.
- Assume the intended reader knows common technical concepts. Explain only project-specific terms or concepts needed by that audience. Include examples and code only when they resolve ambiguity or are requested.
- Prefer shallow headings and short paragraphs. Use a list for parallel items, not for every sentence. Remove empty templates, repeated introductions, and closing sections that only repeat the document.
- Expand only where the reader needs evidence, an implementation step, a decision, or a risk. Do not pad to a word count or cut necessary qualifications to meet an arbitrary length limit. Honor requests for detailed explanations.

## Review and delivery

- Edit existing documents in place; preserve confirmed facts and useful structure. Do not rewrite unrelated sections or add companion documents unless requested.
- Re-read once: check that claims are traceable; names, tables, and diagrams agree; the requested structure is satisfied; acceptance criteria are observable; and repetition is removed.
- After writing the file, reply with its path and the key change. End with one or two lines naming unresolved items or unperformed validation when relevant; do not paste the document again or narrate the writing process.
