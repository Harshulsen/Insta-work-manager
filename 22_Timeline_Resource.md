22_Timeline_Resource.md

«Document Version: 1.0
Status: Approved
Module: Timeline Resource
Priority: Critical»

---

Purpose

The Timeline Resource is the permanent chronological history of every important event that occurs inside the Instagram Workforce Management System (IWMS).

It serves as the system's single source of historical truth.

Whenever administrators need to know what happened, when it happened, who performed it, and why, they should use the Timeline Resource.

---

Philosophy

The Timeline is a history log, not a database.

It never controls business logic.

It only records business events.

Once written, Timeline records are immutable.

---

Responsibilities

The Timeline Resource records:

- Worker lifecycle events
- Training events
- Instagram account events
- Channel link events
- Work events
- Screenshot events
- Review events
- Reward events
- Support events
- Bug reports
- Administrative actions
- Permission changes
- Migration events
- System events

It never replaces the original resource.

---

Ownership

Primary Owner:

Timeline Module

Every module may create Timeline events.

No module may directly modify existing Timeline entries.

---

Resource Lifetime

Property| Value
Created| Immediately after an event
Updated| Never
Archived| Never
Deleted| According to retention policy only

Timeline records are append-only.

---

Timeline Philosophy

One event = One Timeline Entry.

Example:

Worker Registered

↓

Timeline Entry

────────────

Training Assigned

↓

Timeline Entry

────────────

Work Approved

↓

Timeline Entry

Events are never merged.

---

Timeline Identity

Each Timeline entry receives a permanent identifier.

Example:

TL-000001

TL-000002

TL-000003

Timeline IDs are immutable.

---

Primary Fields

Field| Description
Timeline ID| Permanent identifier
Worker ID| Related worker
Event Category| Event type
Event Name| Human-readable event
Related Resource| Linked resource
Created By| Actor
Timestamp| Event time
Metadata| Additional references

---

Event Categories

Supported categories:

- Worker
- Training
- Instagram
- Channel Link
- Profile Photos
- Slot
- Work
- Screenshot
- Review
- Weekly Reward
- Notification
- Support
- Bug Report
- Permission
- Migration
- System

Future categories may be added without redesign.

---

Actor Types

Every Timeline entry records the actor.

Supported actors:

- Worker
- Secondary Admin
- Super Admin
- Automation Engine
- Scheduler
- System
- Migration Tool

---

Event Workflow

Business Event

↓

Timeline Entry

↓

Stored

↓

Searchable

↓

Displayed

Timeline creation should occur immediately after successful business operations.

---

Event Metadata

Timeline entries may include references such as:

- Worker ID
- Work ID
- Review ID
- Screenshot ID
- Reward ID
- Channel Link ID
- Instagram ID
- Support Ticket ID

References should be lightweight.

---

Worker Timeline

Administrators should be able to view the complete worker history.

Example:

Worker Registered

↓

Training Completed

↓

Instagram Assigned

↓

Work Approved

↓

Reward Paid

↓

Account Replaced

↓

Vacation Started

↓

Returned

---

Administrative Timeline

Administrative actions include:

- Permission Granted
- Permission Revoked
- Worker Removed
- Worker Restored
- Reward Override
- Manual Approval
- Link Restoration
- Training Reassignment

---

System Timeline

System-generated events include:

- Daily Scheduler Started
- Health Check Completed
- Backup Created
- Migration Completed
- Broadcast Sent
- Queue Restarted

---

Timeline Views

Supported views:

- Worker Timeline
- Administrator Timeline
- System Timeline
- Season Timeline
- Module Timeline

Views are filters over the same Timeline Resource.

---

Search Support

Search by:

- Timeline ID
- Worker ID
- Event Category
- Event Name
- Related Resource ID
- Actor
- Date Range

Results should support quick navigation to the related resource.

---

Timeline Display Rules

Entries should be displayed in reverse chronological order by default.

Every entry should include:

- Timestamp
- Event
- Actor
- Related Resource
- Quick Actions (where applicable)

---

Worker Visibility

Workers may view only selected Timeline events.

Examples:

- Training Completed
- Work Approved
- Reward Paid
- Vacation Started

Workers should never see:

- Audit-only events
- Internal administrator notes
- Permission changes
- System diagnostics

---

Administrator Visibility

Administrators may view:

- Complete worker timeline
- System timeline (according to permission)
- Module-specific timelines

Permission rules determine visibility.

---

Timeline Integration

Every major module creates Timeline entries.

Examples:

- Worker Module
- Training Module
- Instagram Module
- Work Module
- Review Module
- Reward Module
- Support Module

The Timeline never creates business events.

It only records them.

---

Audit Relationship

Timeline and Audit are different.

Timeline answers:

«What happened?»

Audit answers:

«Who changed what and why?»

Both resources complement each other.

---

Security Rules

Timeline entries are read-only.

No user should edit historical events.

Administrative correction should create a new Timeline entry, never modify an old one.

---

Archive Policy

Timeline entries are permanent.

If retention policies require cleanup:

Entries should first be exported to long-term archive.

---

Backup Policy

Every backup should include:

- Timeline IDs
- Event Metadata
- References
- Timestamps

Timeline restoration must preserve chronological order.

---

Health Check

The Health Checker verifies:

- Broken references
- Invalid timestamps
- Duplicate Timeline IDs
- Missing required metadata

No automatic modification should occur.

---

Performance Guidelines

Timeline entries should remain lightweight.

Store:

- Metadata
- References
- Event summary

Avoid duplicating complete resource data.

---

Resource Relationships

Worker Resource
        │
        ├── Training
        ├── Instagram
        ├── Work
        ├── Review
        ├── Reward
        ├── Support
        └──────────────┐
                       ▼
               Timeline Resource

All major modules publish events to the Timeline.

---

Field Classification

Identity

- Timeline ID

---

Event Information

- Category
- Event Name
- Actor
- Timestamp

---

References

- Worker ID
- Related Resource
- Metadata

---

Future Expansion

Supports:

- Advanced filtering
- Timeline export
- Visual timeline
- AI event summaries
- Cross-worker analytics
- Timeline bookmarks
- Event tagging

---

Database Schema Summary

Timeline

│

├── Timeline ID

├── Worker ID

├── Event Category

├── Event Name

├── Actor

├── Timestamp

├── Related Resource

└── Metadata

---

Edge Cases

- Migration creates historical events.
- Worker permanently deleted.
- Resource restored after deletion.
- Administrator correction.
- System clock change.
- Duplicate event request.

---

Validation Checklist

Before writing:

- Event completed successfully.
- Related resource exists.
- Actor identified.
- Timestamp valid.
- Timeline ID generated.

---

Implementation Checklist

- Timeline ID generation
- Event writer
- Search indexing
- Worker timeline
- Admin timeline
- System timeline
- Module filters
- Archive support
- Backup support

---

TPY Implementation Notes

- Timeline creation should be centralized through a common logging function.
- Store only references and summaries.
- Never allow direct editing of Timeline entries.
- Timeline writes should occur only after successful business transactions.

---

Final Statement

The Timeline Resource is the official historical event log of IWMS.

Every significant action performed by workers, administrators, automation, or the system must generate a Timeline entry.

This resource provides complete historical visibility while remaining immutable, searchable, lightweight, and fully compatible with every operational module.

---

End of 22_Timeline_Resource.md
