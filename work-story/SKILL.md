---
name: work-story
description: Execute a tracked work item end-to-end using a multi-agent workflow. Use when Codex needs to pull a story, bug, task, or similar ticket from Jira or another connected tracker, analyze requirements, choose the right mix of global and repo-local agents, implement the work on a branch, validate it, review it, and move the item to In Review when it is ready.
---

# Work Story

## Overview

Use this skill to work a tracked item from intake through review readiness.
The skill turns a story or bug into an execution brief, selects the right agent mix, drives implementation and verification, and updates the work item when the code is ready for review.

## Workflow

1. Fetch the work item from the named source.
If the user gives a Jira issue key and Jira is connected, use Jira first. Otherwise use the named tracker that Codex can access. See [references/source-adapters.md](references/source-adapters.md) for source selection and fallback rules.

2. Normalize the work item into an execution brief.
Extract the summary, problem, required behavior, acceptance criteria, constraints, dependencies, linked references, and current status. If the ticket is vague, tighten it into concrete, testable outcomes before implementation begins.

3. Build repository context.
Inspect the repository, local [AGENTS.md], test setup, relevant modules, and any repo-local agent definitions. Prefer repository rules and local agent variants when they exist.

4. Choose the agent mix.
Select only the agents the task actually needs. Use [references/agent-selection.md](references/agent-selection.md) to decide between product-owner, researcher, architect, implementer, debugger, tester, and reviewer roles. Prefer repo-local agents over global agents for the same role.

5. Create a work branch.
Do not work on `main` or `master`. Create a branch named after the work item when possible, such as `KAN-123-short-description`.

6. Execute the work.
Implement in bounded steps, commit as useful, and keep the branch coherent. If the story expands, call that out and reduce to the smallest valuable increment that satisfies the stated acceptance criteria.

7. Validate the result.
Run the smallest relevant checks first. Add or update tests when needed to protect the intended behavior and regression surface.

8. Run independent review.
Use a reviewer pass after implementation and testing. Resolve material findings before treating the work as complete.

9. Update the tracker.
When the story is implemented, tested, and reviewed to a working state, update the work item and move it to `In Review`. If the environment supports it, prepare or open a Pull Request targeting `main` or `master`.

## Operating Rules

- Never commit directly to `main` or `master`.
- Do not move the work item to `In Review` if acceptance criteria are still unmet.
- Prefer the smallest working increment over broad scope expansion.
- Use repo-local instructions and agent definitions when they conflict with global defaults.
- Treat tester and reviewer output as quality gates, not optional polish.
- If the work item cannot be fetched from an accessible source, stop and report the missing access or identifier clearly.

## Completion Criteria

Treat the story as ready for `In Review` only when all of the following are true:

- The required behavior matches the normalized acceptance criteria.
- Relevant tests pass, or any missing verification is stated explicitly.
- Reviewer findings are resolved or documented as non-blocking with clear rationale.
- The work exists on a non-`main` branch.
- The tracked item has been updated and transitioned to `In Review`.

## References

- Source handling and tracker fallback: [references/source-adapters.md](references/source-adapters.md)
- Agent selection and default compositions: [references/agent-selection.md](references/agent-selection.md)
