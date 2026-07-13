19_Review_Resource.md

«Document Version: 1.0
Status: Approved
Module: Review Resource
Priority: Critical»

---

Purpose

The Review Resource manages the complete work verification process inside the Instagram Workforce Management System (IWMS).

Its responsibility is to ensure every submitted work package is reviewed consistently, fairly, and with full traceability.

The Review Resource never creates work.

It only evaluates submitted evidence.

---

Philosophy

Work is completed by the worker.

Evidence is submitted through the Screenshot Resource.

The Review Resource decides whether the submitted work satisfies platform requirements.

Every review must be:

- Fair
- Consistent
- Auditable
- Traceable
- Reversible (where permitted)

---

Responsibilities

The Review Resource manages:

- Review Queue
- Review Status
- Review Decision
- Review Notes
- Reviewer Assignment
- Review History
- Timeline Integration
- Audit Integration

It does not manage:

- Work generation
- Screenshot uploads
- Weekly reward calculation
- Worker identity

---

Ownership

Primary Owner:

Review Module

---

Resource Lifetime

Property| Value
Created| After work submission
Updated| During review
Closed| After final decision
Archived| After season completion
Deleted| Never

---

Review Philosophy

One submitted Work Resource creates one Review Resource.

Example:

WRK-10542

↓

REV-10542

Every review belongs to exactly one Work Resource.

---

Review Identity

Each review receives a permanent identifier.

Example:

REV-000001

REV-000002

REV-000003

Review IDs are immutable.

---

Primary Fields

Field| Description
Review ID| Permanent identifier
Work ID| Parent Work
Worker ID| Parent Worker
Reviewer ID| Assigned administrator
Review Status| Current review state
Decision| Final decision
Decision Time| Timestamp
Review Notes| Internal notes

---

Review States

Supported states:

- Pending
- Assigned
- Reviewing
- Approved
- Rejected
- Reopened
- Archived

Only one current state exists.

---

Review Queue

Every submitted work automatically enters the Review Queue.

Work Submitted

↓

Review Queue

↓

Administrator

↓

Review

The queue is ordered chronologically by default.

Future prioritization rules may extend this behavior.

---

Review Workspace

All pending reviews should appear inside the dedicated Screenshot Review Workspace.

Workers should never interact directly with this workspace.

Administrators perform reviews from this centralized interface.

---

Reviewer Assignment

Reviews may be:

- Automatically assigned
- Manually assigned
- Claimed by an authorized administrator (future)

Only one reviewer should actively review a work item at a time.

---

Review Workflow

Pending

↓

Open Review

↓

Inspect Screenshots

↓

Decision

↓

Approve

OR

Reject

↓

Timeline

↓

Worker Notification

---

Review Decision

Supported decisions:

Approved

Work satisfies platform requirements.

Effects:

- Work Status → Approved
- Weekly statistics updated
- Worker notified

---

Rejected

Work does not satisfy requirements.

Effects:

- Work Status → Rejected
- Weekly statistics updated
- Worker notified

Reason should always be recorded.

---

Review Notes

Administrators may record internal notes.

Examples:

- Wrong upload
- Missing reel
- Incorrect account
- Poor quality
- Duplicate screenshot

Review notes are not visible to workers unless explicitly configured in future versions.

---

Bulk Review (Future)

The architecture supports future bulk operations.

Examples:

- Approve multiple works
- Reject multiple works
- Filter by reviewer
- Filter by worker

Bulk operations must create individual Timeline and Audit entries for every affected review.

---

Timeline Integration

Timeline events include:

- Review Created
- Reviewer Assigned
- Review Started
- Review Approved
- Review Rejected
- Review Reopened

---

Audit Integration

Administrative actions requiring audit:

- Manual approval
- Manual rejection
- Review reopening
- Reviewer reassignment
- Decision override

Each audit record includes:

- Administrator
- Review ID
- Worker ID
- Timestamp
- Reason

---

Weekly Reward Integration

Approved reviews contribute to:

- Completed Work
- Weekly Completion Rate
- Performance Statistics

Rejected reviews contribute to:

- Rejected Count
- Quality Statistics

Reward calculation belongs to the Weekly Reward Resource.

---

Search Support

Search by:

- Review ID
- Work ID
- Worker ID
- Reviewer ID

Results should allow:

- Open Worker Profile
- Open Work
- Open Screenshots
- Open Timeline

---

Security Rules

Workers may:

- View final review status.

Workers may not:

- View internal review notes.
- View reviewer identity.
- Modify review decisions.

---

Administrator Permissions

Action| Secondary Admin| Super Admin
View Review| ✅| ✅
Approve| Optional| ✅
Reject| Optional| ✅
Reopen| ❌| ✅
Override Decision| ❌| ✅

---

Archive Policy

After review completion:

Reviews become historical records.

Archived reviews remain available for:

- Timeline
- Analytics
- Worker History
- Audit
- Migration

---

Backup Policy

Backups preserve:

- Review Metadata
- Review Decisions
- Reviewer Assignment
- Work References

Review screenshots remain inside the Screenshot Resource.

---

Health Check

The Health Checker verifies:

- Existing Work
- Existing Worker
- Existing Screenshot References
- Valid Review State
- Missing Decisions
- Broken References

---

Performance Guidelines

The Review Resource stores:

- Decisions
- Metadata
- References

It should never duplicate:

- Screenshots
- Work Packages
- Worker Profiles

---

Resource Relationships

Worker Resource
        │
        ▼
Work Resource
        │
        ▼
Screenshot Resource
        │
        ▼
Review Resource
        │
        ├── Timeline
        ├── Audit
        └── Weekly Reward

---

Field Classification

Identity

- Review ID
- Work ID
- Worker ID

---

Current Configuration

- Review Status
- Decision
- Reviewer

---

Metadata

- Created Time
- Review Time
- Decision Time
- Last Updated

---

Future Expansion

Supports:

- AI-assisted review
- Automatic approval
- Quality scoring
- Reviewer performance metrics
- Smart review routing
- Duplicate detection

---

Database Schema Summary

Review

│

├── Review ID

├── Work ID

├── Worker ID

├── Reviewer ID

├── Status

├── Decision

├── Notes

├── Timeline Reference

└── Audit Reference

---

Edge Cases

- Administrator disconnects during review.
- Two administrators attempt to review the same work.
- Review reopened after approval.
- Missing screenshot file.
- Worker deleted while review is pending.
- Work restored after system recovery.

---

Validation Checklist

Before saving a decision:

- Review exists.
- Work exists.
- Screenshots exist.
- Reviewer has permission.
- Review not already finalized (unless reopening is allowed).

---

Implementation Checklist

- Review ID generation
- Queue management
- Reviewer assignment
- Decision workflow
- Timeline integration
- Audit logging
- Notification triggering
- Archive handling
- Search indexing

---

TPY Implementation Notes

- Store only references to Work and Screenshot resources.
- Do not duplicate screenshot metadata.
- Queue ordering should be configurable.
- Review decisions should trigger automation events rather than directly modifying unrelated resources.

---

Final Statement

The Review Resource is the official specification for work verification within IWMS.

Every approval, rejection, review workflow, reviewer action, and audit process must follow this architecture.

Future enhancements should extend this specification while maintaining compatibility with the Work, Screenshot, Weekly Reward, and Timeline resources.

---

End of 19_Review_Resource.md
