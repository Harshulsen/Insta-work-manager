17_Slot_Resource.md (Part 1)

«Document Version: 1.0
Status: In Progress
Module: Slot Resource
Priority: Critical»

---

Purpose

The Slot Resource manages the complete scheduling system of the Instagram Workforce Management System (IWMS).

It defines when workers receive work, when deadlines expire, when reminders are sent, and how work is distributed throughout the day.

Every Work Resource is created from a Slot Resource.

---

Philosophy

A slot is not a timer.

A slot is a scheduled commitment between the platform and the worker.

Each slot represents one opportunity to perform one work assignment.

---

Responsibilities

The Slot Resource is responsible for:

- Daily work schedule
- Worker slot selection
- Slot validation
- Next slot calculation
- Deadline calculation
- Reminder scheduling
- Vacation integration
- Extra work eligibility
- Scheduler integration

It does not manage:

- Reel packages
- Screenshot reviews
- Weekly rewards
- Worker identity

---

Ownership

Primary Owner:

Slot Module

Only the Slot Module controls slot creation and scheduling.

---

Resource Lifetime

Property| Value
Created| During worker configuration
Updated| When schedule changes
Active| Daily
Archived| On schedule replacement
Deleted| Never directly

---

Slot Philosophy

A worker owns a schedule, not individual temporary slots.

Example:

Worker

↓

Schedule

├── 09:00

├── 13:00

└── 20:00

Every day, these scheduled times generate operational slot instances automatically.

---

Primary Fields

Every Slot Resource should contain:

Field| Description
Slot ID| Permanent identifier
Worker ID| Parent Worker
Slot Time| Scheduled time
Slot Status| Current state
Daily Order| Position within the day
Reminder Status| Reminder progress
Deadline Rule| Deadline calculation method

---

Slot Identity

Each slot receives its own identifier.

Example:

SLT-0001

SLT-0002

SLT-0003

Slot IDs remain permanent even if slot times change.

---

Daily Schedule

Workers may have multiple daily slots.

Example:

09:00

13:00

20:00

The number of slots depends on administrator configuration.

---

Slot Configuration

Administrators define:

- Minimum slots
- Maximum slots
- Allowed slot times
- Slot interval rules

Workers may only choose from approved schedules.

---

Slot Order

Every slot has a daily sequence.

Example:

Slot 1

↓

09:00

──────────

Slot 2

↓

13:00

──────────

Slot 3

↓

20:00

Order is used when calculating the next slot.

---

Current Slot

At any moment, a worker has at most one active slot.

The Scheduler determines the active slot automatically.

---

Next Slot Calculation

Every slot stores a reference to the next scheduled slot.

Example:

09:00

↓

Next

↓

13:00

↓

Next

↓

20:00

This relationship is used to calculate submission deadlines.

---

Deadline Rule

The Work Resource does not calculate deadlines.

The Slot Resource owns this responsibility.

Rule:

Current Slot

↓

Next Slot

↓

30 Minutes Before Next Slot

↓

Submission Deadline

Example:

Current Slot

09:00

↓

Next Slot

13:00

↓

Deadline

12:30

This rule applies automatically to every work assignment.

---

Last Slot of the Day

If there is no later slot on the same day:

The system follows the project-wide end-of-day deadline policy defined by the Scheduler.

The exact policy is configured centrally and should not be hard-coded into the Slot Resource.

---

Slot Status

Supported states:

- Scheduled
- Active
- Completed
- Missed
- Skipped
- Cancelled
- Vacation

The current status is stored here.

History belongs to the Timeline Resource.

---

Current Scope

This part defines:

- Purpose
- Ownership
- Slot Identity
- Daily Schedule
- Slot Order
- Next Slot
- Deadline Calculation
- Slot States

The following parts will define:

- Reminder Engine
- Temporary Schedule Changes
- Vacation Mode
- Extra Work
- Scheduler Integration
- Timeline
- Audit
- Migration
- Recovery
- Final Specification

---

End of Part 1

17_Slot_Resource.md (Part 2)

«Document Version: 1.0
Status: In Progress
Module: Slot Resource
Priority: Critical»

---

Reminder System

The Slot Resource is responsible for scheduling reminders.

Reminder delivery is handled by the Notification Module.

The Slot Resource only determines when reminders should occur.

---

Reminder Types

Supported reminder categories:

- Upcoming Slot Reminder
- Work Pending Reminder
- Submission Deadline Reminder
- Missed Work Notification

Future reminder types may be added without redesigning the resource.

---

Reminder Workflow

Slot

↓

Reminder Schedule

↓

Notification Queue

↓

Worker

The Slot Resource never sends notifications directly.

---

Slot Activation

At the scheduled time:

The Scheduler performs:

1. Validate Worker.
2. Validate Worker State.
3. Validate Instagram Accounts.
4. Validate Training.
5. Generate Work Resource.
6. Deliver Work Package.

Only then does the slot become Active.

---

Slot Completion

A slot is completed when:

- Work has been submitted successfully, or
- The submission deadline expires.

Completion does not imply approval.

Approval belongs to the Review Module.

---

Temporary Schedule Change

Workers may temporarily modify their schedule if allowed.

Examples:

- Today only
- Until a specified date
- Administrator-defined duration

Temporary schedules automatically expire.

---

Temporary Schedule Workflow

Current Schedule

↓

Temporary Change

↓

Temporary Active

↓

Expiration

↓

Original Schedule Restored

The original schedule is preserved.

---

Vacation Mode

Vacation temporarily disables slot generation.

During Vacation:

- No new Work Resources.
- No reminders.
- No missed work.
- Worker remains registered.

When Vacation ends:

The next valid slot becomes active automatically.

---

Extra Work Eligibility

Administrators may enable optional Extra Work.

Eligibility checks include:

- Worker is Active.
- No pending work.
- No missed submission in progress.
- Current schedule permits extra work.

If all conditions are satisfied:

An additional Work Resource may be generated.

---

Skipped Slots

A slot may be skipped when:

- Vacation is active.
- Maintenance Mode is active.
- Administrator skips the slot.
- Worker is suspended.

Skipped slots do not count as missed work.

---

Maintenance Integration

During Maintenance Mode:

Scheduled slots remain recorded.

However:

- No Work Resources are generated.
- No reminders are delivered.
- Deadlines do not begin.

After maintenance:

Scheduling resumes from the next applicable slot according to the Scheduler policy.

---

Scheduler Integration

The Scheduler continuously monitors:

- Current time
- Worker state
- Slot schedule
- Temporary changes
- Vacation status

The Scheduler decides when a slot becomes active.

The Slot Resource stores the scheduling configuration.

---

Work Dependency

Every active slot generates exactly one Work Resource.

Relationship:

Slot

↓

Work Resource

If work generation fails:

The Scheduler should retry according to system policy.

---

Timeline Integration

The following events create Timeline entries:

- Slot Created
- Slot Updated
- Temporary Schedule Enabled
- Temporary Schedule Ended
- Vacation Started
- Vacation Ended
- Slot Activated
- Slot Completed
- Slot Skipped

Timeline remains append-only.

---

Audit Integration

Administrative actions requiring audit:

- Manual Slot Change
- Forced Slot Activation
- Manual Skip
- Vacation Override
- Schedule Replacement

Audit records should include:

- Administrator
- Timestamp
- Worker ID
- Slot ID
- Reason

---

Search Integration

Supported searches:

- Slot ID
- Worker ID
- Schedule
- Season

Results should provide:

- Worker Profile
- Slot Details
- Related Work
- Timeline

---

Remaining Sections

The final part will define:

- Migration
- Security
- Health Checks
- Recovery
- Resource Diagram
- Field Classification
- Performance Guidelines
- Future Expansion
- Implementation Notes
- Final Specification

---

End of Part 2

17_Slot_Resource.md (Part 3)

«Document Version: 1.0
Status: Approved
Module: Slot Resource
Priority: Critical»

---

Migration Support

The Slot Resource must support seamless migration between bot versions.

Migration should preserve:

- Slot ID
- Worker Reference
- Daily Schedule
- Slot Order
- Temporary Schedule
- Vacation Status
- Current Configuration

The worker should continue using the same schedule after migration.

---

Recovery Policy

If a scheduling error occurs:

Administrators may restore:

- Previous Schedule
- Temporary Schedule
- Vacation Configuration

Recovery should never create duplicate slots.

Existing Work Resources remain unchanged.

---

Health Check Rules

The Health Checker should verify:

- Worker reference exists.
- Schedule is valid.
- Slot order is continuous.
- Next-slot references are valid.
- Deadline rules are valid.
- Temporary schedules have valid expiration dates.
- Vacation status is consistent.

Problems should be reported instead of automatically corrected.

---

Resource Integrity Rules

Every Slot Resource must satisfy:

✓ Existing Worker

✓ Valid Schedule

✓ Valid Slot Order

✓ Valid Next Slot Reference

✓ Valid Status

✓ Valid Deadline Rule

Invalid slot configurations must never become active.

---

Security Rules

Workers may:

- View their own schedule.
- Request schedule changes (if enabled).
- Enable Vacation Mode (if allowed).
- View next slot information.

Workers may not:

- Modify restricted schedules.
- Change administrator-defined limits.
- Edit slot order.
- Override deadlines.

---

Administrator Permissions

Action| Secondary Admin| Super Admin
View Schedule| ✅| ✅
Edit Schedule| Optional| ✅
Enable Vacation| Optional| ✅
Disable Vacation| Optional| ✅
Skip Slot| Optional| ✅
Force Slot Activation| ❌| ✅
Change Global Slot Rules| ❌| ✅

Permission policies are managed by the Permission Module.

---

Archive Policy

Previous schedules should be archived whenever:

- Permanent schedule changes occur.
- Administrator replaces a schedule template.

Archived schedules remain available for:

- Timeline
- Audit
- Migration
- Historical Review

Archived schedules are never reactivated automatically.

---

Backup Policy

Backups should preserve:

- Schedule
- Slot Order
- Vacation Status
- Temporary Schedule
- Deadline Rules

Operational slot instances should be regenerated after restoration when appropriate.

---

Performance Guidelines

The Slot Resource should store only scheduling metadata.

It should never contain:

- Reel Packages
- Screenshot Files
- Review Results
- Training Media

These belong to their respective resources.

---

Search Optimization

Supported searches:

- Slot ID
- Worker ID
- Daily Time
- Schedule Group
- Season

Search results should allow quick navigation to:

- Worker Profile
- Schedule Details
- Related Work
- Timeline

---

Resource Relationships

Worker Resource
        │
        ▼
Slot Resource
        │
        ├── Scheduler
        ├── Work Resource
        ├── Notification Resource
        ├── Timeline
        └── Vacation Configuration

The Slot Resource defines scheduling.

The Scheduler executes it.

---

Field Classification

The Slot Resource contains three logical groups.

Identity

- Slot ID
- Worker Reference

---

Current Configuration

- Slot Time
- Slot Order
- Next Slot
- Deadline Rule
- Vacation Status
- Temporary Schedule

---

Metadata

- Created Date
- Updated Date
- Last Activated
- Last Completed

Historical events remain in the Timeline Resource.

---

Future Expansion

The Slot Resource supports future capabilities.

Examples:

- Multiple Shift Templates
- Campaign-specific Schedules
- AI Schedule Optimization
- Regional Time Zones
- Public Holiday Rules
- Dynamic Slot Balancing
- Seasonal Workloads

These features should integrate without redesigning the existing architecture.

---

Implementation Notes

Resource Type

Operational Resource

---

Primary Owner

Slot Module

---

Parent Resource

Worker Resource

---

Search Indexed

Yes

---

Timeline Enabled

Yes

---

Audit Enabled

Yes

---

Migration Supported

Yes

---

Backup Required

Yes

---

Versioned

No

Schedule templates may be versioned separately.

---

Archive Supported

Yes

---

Recovery Supported

Yes

---

Cache Friendly

Yes

Only current schedule summaries should be cached.

---

Final Specification Summary

The Slot Resource defines the scheduling backbone of IWMS.

It manages:

- Daily schedules
- Deadline calculations
- Vacation mode
- Temporary schedule changes
- Scheduler integration
- Reminder timing
- Work generation triggers

while delegating work execution, notifications, and reviews to their dedicated resources.

This architecture ensures:

- Predictable scheduling
- Consistent deadline calculation
- Flexible worker scheduling
- High scalability
- Reliable automation
- Migration compatibility

---

Final Statement

The Slot Resource is the official specification for scheduling within IWMS.

Every work assignment, reminder, deadline, vacation period, and scheduling decision must comply with this specification.

Any future enhancement affecting scheduling behavior must extend this architecture while maintaining compatibility with existing Worker and Work Resources.

---

End of 17_Slot_Resource.md
