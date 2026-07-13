25_Bug_Report_Resource.md

«Document Version: 1.0
Status: Approved
Module: Bug Report Resource
Priority: Critical»

---

Purpose

The Bug Report Resource manages every technical issue reported by workers and administrators within the Instagram Workforce Management System (IWMS).

Unlike the Support Resource, which handles assistance requests, the Bug Report Resource is dedicated exclusively to identifying, tracking, investigating, and resolving software defects.

Each bug report becomes a structured engineering record that can be investigated without cluttering administrator chats.

---

Philosophy

Support answers:

«"How do I use the system?"»

Bug Reports answer:

«"The system is not working correctly."»

Every bug should be tracked until it is:

- Fixed
- Rejected
- Confirmed as duplicate
- Deferred

---

Responsibilities

The Bug Report Resource manages:

- Bug reporting
- Screenshot collection
- Error description
- Reproduction information
- Bug status
- Priority
- Resolution tracking
- Timeline integration
- Audit integration

It does not manage:

- Support conversations
- Worker performance
- Review workflow
- Rewards

---

Ownership

Primary Owner:

Bug Report Module

---

Resource Lifetime

Property| Value
Created| When a bug is reported
Updated| During investigation
Resolved| After the issue is fixed
Archived| After verification
Deleted| Never

---

Bug Report Philosophy

One software issue creates one Bug Report.

Example:

Worker

↓

Bug Report

↓

Investigation

↓

Fixed

---

Bug Report Identity

Each report receives a permanent identifier.

Example:

BUG-000001

BUG-000002

BUG-000003

IDs are immutable.

---

Primary Fields

Field| Description
Bug ID| Permanent identifier
Reporter ID| Worker/Admin
Related Worker| Optional
Status| Current bug status
Priority| Bug priority
Category| Bug type
Screenshot Reference| Evidence
Description| Problem summary
Assigned Developer/Admin| Current owner

---

Bug Categories

Supported categories:

- Login Issue
- Training Issue
- Work Issue
- Screenshot Upload
- Review System
- Reward Calculation
- Notification Issue
- UI Issue
- Performance Issue
- System Error
- Other

---

Priority Levels

Supported priorities:

- Low
- Medium
- High
- Critical

Critical bugs should immediately notify administrators.

---

Bug States

Supported states:

- Reported
- Confirmed
- Investigating
- Waiting Information
- Fixed
- Verified
- Rejected
- Duplicate
- Archived

---

Reporting Workflow

Worker

↓

Report Bug

↓

Description

↓

Screenshot

↓

Bug Group

↓

Investigation

↓

Resolution

↓

Closed

---

Bug Report Group

Every new report should automatically appear in a dedicated Telegram Bug Report Group.

The group should contain:

- Bug ID
- Reporter
- Worker Profile Shortcut
- Description
- Screenshot
- Device Information (if available)
- Bot Version
- Timestamp

Administrators should never need to search private chats for bug reports.

---

Screenshot Evidence

Bug reports may include:

- Screenshot
- Screen recording
- Logs (future)
- Error message
- Additional attachments

Evidence remains attached to the Bug Report.

---

Related Resources

A bug may reference:

- Worker
- Work
- Review
- Screenshot
- Training
- Notification
- Support Ticket

References help developers reproduce issues.

---

Timeline Integration

Timeline events include:

- Bug Reported
- Bug Confirmed
- Investigation Started
- Additional Information Requested
- Bug Fixed
- Bug Verified
- Bug Closed

---

Audit Integration

Audit required for:

- Priority override
- Manual closure
- Status override
- Duplicate merge
- Report deletion (if ever permitted)

---

Search Support

Search by:

- Bug ID
- Worker ID
- Category
- Status
- Priority

Results should allow:

- Open Worker Profile
- Open Related Resource
- Open Timeline

---

Worker Permissions

Workers may:

- Report bugs.
- Upload screenshots.
- Reply when additional information is requested.
- View bug status.

Workers may not:

- Edit submitted reports.
- Delete reports.
- Change priority.

---

Administrator Permissions

Action| Secondary Admin| Super Admin
View Bug| ✅| ✅
Reply| Optional| ✅
Change Status| Optional| ✅
Change Priority| ❌| ✅
Close Bug| ❌| ✅

---

Archive Policy

Resolved bug reports become archived.

Archived reports remain available for:

- Timeline
- Analytics
- Release Notes
- Audit
- Future Investigation

---

Backup Policy

Backups preserve:

- Bug Metadata
- Evidence References
- Status History
- Timeline References

---

Health Check

The Health Checker verifies:

- Existing reporter
- Existing related resources
- Broken evidence references
- Invalid status transitions
- Duplicate Bug IDs

---

Performance Guidelines

The Bug Report Resource stores:

- Metadata
- References
- Evidence references

It should never duplicate complete Worker, Work, or Timeline records.

---

Resource Relationships

Worker Resource
        │
        ▼
Bug Report Resource
        │
        ├── Bug Report Group
        ├── Timeline
        ├── Audit
        ├── Notification
        └── Related Resources

---

Field Classification

Identity

- Bug ID
- Reporter ID

---

Configuration

- Category
- Priority
- Status
- Assigned Administrator

---

Metadata

- Created Time
- Updated Time
- Fixed Time
- Verified Time

---

Future Expansion

Supports:

- Automatic crash reports
- Error log attachment
- AI bug classification
- Duplicate detection
- Version tracking
- Release milestone linking
- Internal developer notes

---

Database Schema Summary

Bug Report

│

├── Bug ID

├── Reporter ID

├── Category

├── Priority

├── Status

├── Evidence References

├── Timeline Reference

└── Audit Reference

---

Edge Cases

- Same bug reported by multiple workers.
- Screenshot missing.
- Worker deleted after reporting.
- Duplicate reports.
- Bug fixed before investigation.
- Bug cannot be reproduced.

---

Validation Checklist

Before creating a Bug Report:

- Reporter exists.
- Description provided.
- Bug ID generated.
- Category selected.
- Required evidence attached (if configured).

---

Implementation Checklist

- Bug ID generation
- Bug report group integration
- Screenshot support
- Status workflow
- Priority management
- Timeline integration
- Audit logging
- Archive handling
- Search indexing

---

TPY Implementation Notes

- Bug reports should be bridged between workers and the dedicated Bug Report Group.
- Store Telegram message IDs for synchronization and reply mapping.
- Evidence should be referenced by Telegram "file_id" where possible.
- Status updates should automatically notify the reporter.

---

Final Statement

The Bug Report Resource is the official specification for technical issue management within IWMS.

Every reported bug, investigation, status update, evidence attachment, and resolution must comply with this architecture, providing a structured engineering workflow, complete traceability, and seamless integration with Timeline, Audit, Notification, and related operational resources.

---

End of 25_Bug_Report_Resource.md
