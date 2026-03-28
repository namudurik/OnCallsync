# MVP Scope and Build Plan (Google Calendar On-Call)

This document defines the smallest build that can support paid pilots.

## MVP objective

Deliver one clear promise:

"Your on-call schedule is generated, published to Google Calendar, and kept
accurate when swaps happen."

## In-scope (MVP v1)

1. Team setup
   - Team name
   - Time zone
   - Rotation members and order
   - Rotation cadence (daily or weekly)

2. Schedule generation
   - Generate future on-call shifts for a configurable horizon (for example 8-12
     weeks)
   - Skip/adjust for member unavailability windows

3. Google Calendar sync
   - Create/update events in a selected Google Calendar
   - Clear, consistent event title format (for example: `On-call: {Engineer}`)
   - Event description includes source metadata for reliable updates

4. Swap handling
   - Support one-off swaps between two members
   - Update affected calendar events immediately
   - Maintain audit log of who swapped and when

5. Basic notifications
   - Daily summary email or Slack message (one integration is enough for v1)
   - Alert for uncovered shift

## Explicitly out of scope (v1)

- PagerDuty/Opsgenie deep bi-directional sync
- Sophisticated fairness algorithms beyond simple rotation rules
- Multi-team dashboards
- Mobile app
- Complex approval workflows

## Technical architecture (lean)

Suggested stack (optimize for speed and reliability):

- Backend: TypeScript + Node.js
- API: REST endpoints for setup, schedule generation, swaps
- Data store: Postgres (or SQLite for first pilot if needed)
- Job runner: background worker for sync and notifications
- Integration: Google Calendar API with OAuth 2.0

## Core data model

- `teams`: id, name, timezone
- `members`: id, team_id, name, email, active
- `rotations`: id, team_id, cadence, start_at
- `shifts`: id, team_id, member_id, starts_at, ends_at, status
- `swaps`: id, team_id, shift_id, from_member_id, to_member_id, created_at
- `calendar_events`: id, shift_id, provider_event_id, last_synced_at

## Key reliability rules

1. Sync idempotency
   - Re-running sync should not create duplicate events.
2. Source of truth
   - Internal `shifts` table is authoritative, calendar is projection.
3. Auditability
   - Every manual change (swap, override) is logged.

## Acceptance tests before pilot go-live

1. Rotation generation test
   - Given 6 members and weekly cadence, 12 weeks of shifts are generated with no
     gaps.
2. Calendar sync test
   - Creating shifts produces matching Google Calendar events.
3. Update test
   - Changing one shift updates exactly one calendar event.
4. Swap test
   - One-off swap changes owner and updates calendar within acceptable latency.
5. Failure retry test
   - Temporary Google API failure retries without data corruption.

## Build sequence

1. Build internal schedule engine and data model.
2. Add Google Calendar event create/update sync.
3. Add swap workflow and audit log.
4. Add minimal admin UI or CLI for pilot operations.
5. Run acceptance tests with synthetic data.
6. Onboard first pilot team manually.

## Pilot implementation strategy

Prefer "concierge onboarding" for first pilots:

- You handle setup manually.
- Customers validate outcomes, not onboarding UX.
- Product learns from real schedules before automation.

## Decision gate after first 3 pilots

Continue scaling only if:

- Teams keep weekly active use
- At least one painful workflow is eliminated (for example: manual swap chaos)
- Customers confirm renewal intent at target price band
