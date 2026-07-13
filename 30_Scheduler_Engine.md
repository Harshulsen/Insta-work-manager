30_Scheduler_Engine.md

«Document Version: 1.0
Status: Approved
Module: Scheduler Engine
Priority: Critical»

---

Purpose

The Scheduler Engine is responsible for executing every time-based operation inside the Instagram Workforce Management System (IWMS).

It continuously monitors time, worker schedules, and system state to ensure every task executes at the correct moment.

The Scheduler Engine is the platform's official time controller.

---

Philosophy

The Scheduler Engine does not own business logic.

It only determines when something should happen.

The Automation Engine determines what should happen.

Business Resources determine how data is managed.

---

Responsibilities

The Scheduler Engine manages:

- Slot activation
- Work scheduling
- Deadline monitoring
- Reminder scheduling
- Temporary schedule expiration
- Vacation expiration
- Retry scheduling
- Queue scheduling
- Time-based automation triggers

It does not manage:

- Worker data
- Reviews
- Rewards
- Permissions
- Business resources

---

Ownership

Primary Owner:

Scheduler Module

---

Core Principles

The Scheduler must be:

- Time-driven
- Deterministic
- Fault-tolerant
- Restart-safe
- Idempotent
- Resource-independent

Time should always be the only trigger.

---

Scheduler Workflow

Current Time

↓

Scheduled Events

↓

Eligible Events

↓

Automation Engine

↓

Execution

---

Managed Schedules

The Scheduler monitors:

- Daily Slots
- Reminder Times
- Submission Deadlines
- Temporary Permissions
- Vacation End Dates
- Maintenance Windows
- Backup Schedules
- Health Checks
- Cleanup Tasks

---

Slot Activation

At the configured slot time:

The Scheduler should:

1. Validate Worker.
2. Validate Schedule.
3. Validate System Status.
4. Trigger Work Generation.

The Scheduler never creates Work Resources directly.

---

Deadline Monitoring

The Scheduler continuously verifies:

Current Time

↓

Submission Deadline

↓

Expired?

↓

Mark Missed

↓

Notify Automation

Deadline calculation remains owned by the Slot Resource.

---

Reminder Scheduling

Supported reminders:

- Upcoming Slot
- Work Reminder
- Submission Reminder
- Support Reminder
- Pending Review Reminder
- Administrative Reminder

The Scheduler triggers reminder events.

Notification delivery belongs to the Notification Resource.

---

Temporary Schedule Expiration

When a temporary schedule expires:

Temporary Schedule

↓

Expiration Time

↓

Restore Original Schedule

The Scheduler performs only the trigger.

---

Vacation Monitoring

The Scheduler automatically checks:

- Vacation Start
- Vacation End

When vacation ends:

The worker automatically rejoins the normal schedule.

---

Maintenance Mode

During maintenance:

The Scheduler may pause:

- Slot activation
- Reminder generation
- Background automation

System health monitoring should continue.

---

Retry Scheduling

Failed automation jobs may request retry scheduling.

The Scheduler maintains:

- Retry Time
- Retry Count
- Retry Eligibility

Execution remains the responsibility of the Automation Engine.

---

Health Check Scheduling

The Scheduler periodically starts:

- Database validation
- Queue validation
- Broken reference detection
- Resource integrity checks

Health analysis belongs to the Health Check System.

---

Backup Scheduling

Configured backup schedules include:

- Daily
- Weekly
- Manual
- Emergency

The Scheduler starts backup events according to configuration.

---

Cleanup Scheduling

The Scheduler may trigger:

- Temporary cache cleanup
- Expired notification cleanup
- Session cleanup
- Temporary resource cleanup

Permanent business resources should never be removed automatically unless explicitly configured.

---

Timeline Integration

Timeline events include:

- Scheduler Started
- Scheduler Stopped
- Slot Activated
- Reminder Triggered
- Deadline Triggered
- Vacation Ended
- Retry Scheduled

---

Audit Integration

Audit records required for:

- Manual scheduler override
- Manual deadline adjustment
- Manual retry execution
- Manual maintenance activation

---

Search Support

Search by:

- Scheduled Event ID
- Worker ID
- Trigger Time
- Event Type
- Status

---

Security Rules

The Scheduler:

- Must validate system state.
- Must never bypass permissions.
- Must not modify protected resources directly.
- Must execute only configured events.

---

Health Monitoring

The Scheduler continuously verifies:

- Clock synchronization
- Delayed executions
- Missed executions
- Queue backlog
- Long-running events

Critical failures should notify administrators immediately.

---

Performance Guidelines

The Scheduler should:

- Minimize CPU usage.
- Avoid unnecessary polling.
- Batch compatible checks.
- Recover cleanly after restart.

---

Resource Relationships

Scheduler Engine
        │
        ├── Slot Resource
        ├── Automation Engine
        ├── Notification Resource
        ├── Health Check
        ├── Backup System
        ├── Timeline
        └── Audit

The Scheduler triggers operations but does not own business data.

---

Future Expansion

Supports:

- Distributed schedulers
- Time zone support
- Priority scheduling
- Cron-like expressions
- AI load balancing
- High-availability scheduling

---

Database Schema Summary

Scheduled Event

│

├── Event ID

├── Event Type

├── Trigger Time

├── Status

├── Retry Information

├── Timeline Reference

└── Audit Reference

---

Edge Cases

- Server restart during scheduled execution.
- Duplicate scheduler instance.
- System clock adjustment.
- Missed execution after downtime.
- Maintenance starts during slot activation.
- Worker removed before scheduled event.

---

Validation Checklist

Before triggering an event:

- Current time valid.
- Event active.
- Related resource exists.
- System not paused.
- Duplicate execution prevented.

---

Implementation Checklist

- Scheduler loop
- Event dispatcher
- Slot monitoring
- Reminder scheduler
- Deadline monitor
- Retry scheduler
- Backup scheduler
- Health check scheduler
- Timeline integration

---

TPY Implementation Notes

- The Scheduler should only generate events and delegate execution to the Automation Engine.
- Time comparisons should use a consistent server time source.
- Every scheduled execution should have a unique execution identifier for debugging.
- After bot restart, the Scheduler should safely recover pending events without duplicating completed actions.

---

Final Statement

The Scheduler Engine is the official time-management framework of IWMS.

Every slot activation, reminder, deadline, retry, backup, cleanup task, and scheduled automation event must be coordinated through this engine, ensuring precise, reliable, and scalable time-based execution across the platform.

---

End of 30_Scheduler_Engine.md
