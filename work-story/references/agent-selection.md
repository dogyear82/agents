# Agent Selection

Use this reference to choose the smallest useful multi-agent composition for a tracked work item.

## Selection Rules

- Prefer repo-local agents over global agents when both define the same role.
- Do not spawn every available agent by default.
- Select agents based on ambiguity, technical risk, and verification needs.
- Keep planning, implementation, testing, debugging, and review concerns distinct when that separation improves quality.

## Role Triggers

### product_owner

Use when the ticket is ambiguous, missing acceptance criteria, or likely too broad.

Expected output:
- clarified goal
- scope boundaries
- acceptance criteria
- risks and dependencies

### researcher

Use when the codebase area is unfamiliar or the impact surface is unclear.

Expected output:
- relevant files and flows
- constraints and dependencies
- likely implementation surface

### architect

Use when the story crosses module boundaries, changes interfaces, or introduces non-trivial design tradeoffs.

Expected output:
- recommended design approach
- tradeoffs
- migration or sequencing guidance

### implementer

Use for bounded code changes once the task is clear enough to execute.

Expected output:
- working code
- focused diffs
- relevant verification

### debugger

Use when expected behavior is failing, the story exposes a regression, or the root cause is not obvious.

Expected output:
- reproduced issue or narrowed failure surface
- root cause
- minimal fix path

### tester

Use when behavior needs stronger verification, regression coverage, or clearer boundary-case coverage.

Expected output:
- tests added or improved
- gaps in confidence
- verification evidence

### reviewer

Use after implementation and testing for an independent quality pass.

Expected output:
- prioritized findings or explicit no-findings result
- residual risks

## Default Compositions

### Small bug fix

- implementer
- tester
- reviewer

Add `debugger` if reproduction or root cause is unclear.

### Ambiguous feature story

- product_owner
- researcher
- implementer
- tester
- reviewer

Add `architect` if the change crosses boundaries or needs interface decisions.

### Cross-cutting refactor or platform story

- researcher
- architect
- implementer
- tester
- reviewer

Add `product_owner` when scope needs to be reduced to a workable increment.

## Exit Rule

Do not treat the story as complete until reviewer feedback is resolved and the implemented behavior matches the normalized acceptance criteria closely enough to move the work item to `In Review`.
