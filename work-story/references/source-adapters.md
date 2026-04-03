# Source Adapters

Use this reference when deciding where to fetch and update the work item.

## Source Priority

1. If the user names a tracker explicitly, use that tracker if Codex has access.
2. If the identifier is a Jira-style issue key and Jira is connected, use Jira.
3. If multiple accessible trackers are available and the user did not specify one, use the tracker that contains the referenced item.
4. If no accessible tracker can provide the item, stop and report the missing source clearly.

## Jira Workflow

When Jira is available:

- Fetch the issue summary, description, comments, linked docs, attachments, issue type, status, and transitions.
- Extract acceptance criteria from the description or linked material.
- Add comments only when they materially help trace progress or handoff.
- Move the issue to `In Review` only after implementation, testing, and review are complete.

## Non-Jira Trackers

If the work item lives somewhere other than Jira:

- Use the accessible source the user names.
- Reconstruct the same execution brief used for Jira items: problem, outcome, acceptance criteria, constraints, dependencies, and current status.
- If tracker write-back is supported, update status to the equivalent of `In Review`.
- If tracker write-back is not supported, report readiness and state that the status move could not be performed.

## Missing or Weak Tickets

If the story is poorly defined:

- Normalize it before coding.
- Identify non-goals and assumptions explicitly.
- Use the product-owner role when the ticket needs sharper scope, priority, or acceptance criteria.

## Update Discipline

- Avoid noisy progress comments.
- Record blockers when they affect scope, timeline, or handoff.
- Prefer concise updates that explain what was implemented, how it was verified, and why the item is now ready for review.
