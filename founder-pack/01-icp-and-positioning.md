# ICP and Positioning

## Target wedge (start here)

Primary ICP:

- Engineering teams with 5-40 engineers
- Already using Google Calendar as a source of truth
- On-call managed manually (spreadsheets, recurring events, Slack threads)
- At least weekly schedule changes (swaps, PTO, incidents, handoff edits)

Secondary ICP (later):

- SRE-heavy teams with stricter escalation policies
- Teams currently using PagerDuty/Opsgenie but frustrated by schedule admin

## Core problem statement

"Our on-call schedule in Google Calendar is constantly wrong because changes are
manual, and the person on-call is unclear during swaps/PTO/handoffs."

## Value proposition

OnCallsync automatically keeps on-call rotations accurate in Google Calendar so
tech teams stop losing time to schedule admin and misrouted incidents.

## Positioning formula

For [ICP], who currently [manual workaround], OnCallsync is a [product category]
that [primary outcome]. Unlike [alternative], it [differentiator].

Filled example:

For engineering teams using Google Workspace who manually maintain on-call
events, OnCallsync is a Google Calendar-native on-call scheduler that keeps
rotations accurate during swaps and PTO. Unlike spreadsheet or ad hoc calendar
management, it updates schedules automatically with clear ownership.

## Jobs-to-be-done

Functional jobs:

- Publish an always-correct on-call schedule in Google Calendar
- Handle swaps/PTO quickly without admin overhead
- Make "who is on-call now" obvious to everyone

Emotional jobs:

- Reduce anxiety about missed pages due to schedule mistakes
- Avoid fire drills caused by stale calendar events

Social jobs:

- Show leadership that incident readiness is controlled and reliable

## Why teams buy

- Fewer misroutes and escalation delays
- Less manager/admin toil every week
- Faster handoffs and less confusion during incidents

## Why teams do not buy (objections)

- "We already have PagerDuty schedules"
- "This feels like a nice-to-have, not urgent"
- "Integrations/security review is too heavy"

## Objection handling notes

- If they have PagerDuty: frame as Google Calendar visibility + admin automation.
- If "nice-to-have": quantify weekly admin hours and incident confusion cost.
- If security concern: keep scope minimal, document OAuth scopes clearly.

## Disqualifiers (do not spend cycles)

- Teams not using Google Calendar operationally
- Teams with no recurring on-call process
- Teams with less than monthly schedule changes

## Validation checkpoints

- At least 70% of interviews report recurring schedule pain
- At least 30% agree to paid pilot discussion
- Repeated top-3 pains appear across teams (not one-off edge cases)
