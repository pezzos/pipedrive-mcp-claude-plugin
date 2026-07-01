---
name: pipedrive-complete-activity
description: Use with the custom Pipedrive MCP tools when the user says an activity, task, call, meeting, reminder, follow-up, or email todo has been done, should be marked done, rescheduled, postponed, or updated in Pipedrive. Do not use the official Pipedrive connector.
---

# Pipedrive Complete Activity

This skill is for the custom **Pipedrive MCP** desktop extension. Use only MCP
tools whose names start with `pipedrive_`, such as `pipedrive_health_check`,
`pipedrive_mark_activity_done`, and `pipedrive_reschedule_activity`. Do not use
Anthropic's official Pipedrive connector, generic Pipedrive integrations,
browser automation, or direct web/API calls.

If no `pipedrive_` tools are available, stop and tell the operator that the
Pipedrive MCP desktop extension is not connected. Do not continue with the
official Pipedrive connector.

Use this skill for requests like "j'ai fait l'appel avec Jean", "marque cette relance comme faite", "l'email est parti", "reporte cette tâche à vendredi", or "mets à jour cette activité".

## Resolve The Activity

Find the open activity from the user's context:

- Search by person, organization, deal, lead, subject, type, and due date.
- Prefer open and overdue activities.
- If several activities match, present a shortlist and ask which one to use.

Do not mark an ambiguous activity as done.

## Choose The Operation

- Done/completed/finished -> `pipedrive_mark_activity_done`.
- Postpone/reschedule/change date -> `pipedrive_reschedule_activity`.
- Update subject, note, type, or links -> `pipedrive_update_activity`.

After completion, offer to create a follow-up only when it is useful. Use the add activity or email activity workflow for the follow-up.

## Write Safely

Always run the selected tool with `dry_run=true` first. Show the target activity ID, current subject/date, and proposed change. Execute with `dry_run=false` only after explicit approval.
