# Contributing

Thank you for helping test and improve Context-First Agent Workflows.

## Before you contribute

- Do not submit proprietary source code, internal project names, customer data, credentials, private URLs, logs, or screenshots containing sensitive information.
- Do not claim a productivity improvement without describing the task, baseline, environment, and measurement method.
- Prefer concrete counterexamples over abstract disagreement. A rule that fails in a real repository is valuable evidence.

## Useful contribution types

1. **Sanitized case studies** using the [benchmark protocol](benchmarks/task-protocol.md).
2. **Agent adapters** that preserve the intent of the skills for another coding-agent platform.
3. **Clarifications and corrections** to guidance that is ambiguous or too rigid.
4. **Examples** of module boundaries, public contracts, or validation handoff.
5. **Counterexamples** where `app + modules + tools`, project maps, or minimal-context execution need qualification.

## Proposing a change

For small wording fixes or examples, open a focused pull request.

For changes to skill behavior, structural rules, or the methodology:

1. Open a Discussion or Issue describing the problem, task type, ecosystem, and observed failure mode.
2. State the proposed rule change and its trade-offs.
3. Include a sanitized code sketch or case study when possible.
4. Keep the proposed change compatible with the core separation of structure, navigation, and execution unless there is evidence that the separation itself is flawed.

## Pull request guidance

- Keep one conceptual change per pull request.
- Explain which skill or document changes and why.
- Preserve Markdown readability and short operational instructions.
- Do not add unrequested dependencies, generated output, or platform-specific files outside the scope of the contribution.
- If changing a skill, update its examples or corresponding documentation where needed.

## Case study disclosure

Use generic names such as `orders`, `billing`, `recordings`, or `identity`. Replace identifiers, URLs, payloads, logs, organization names, and domain data with synthetic values. State limitations clearly.

By submitting a contribution, you agree that it may be distributed under the repository's Apache License 2.0.
