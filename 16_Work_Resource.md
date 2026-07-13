16_Work_Resource.md (Part 1)

«Document Version: 1.0
Status: In Progress
Module: Work Resource
Priority: Critical»

---

Purpose

The Work Resource manages every work assignment delivered to workers within the Instagram Workforce Management System (IWMS).

It is the operational core of the platform.

Every assigned reel, screenshot submission, review, work history, and weekly reward originates from the Work Resource.

---

Philosophy

A Work Resource represents one scheduled work assignment.

It should contain everything required to complete that assignment while remaining independent from other work assignments.

Every work assignment should be:

- Traceable
- Reviewable
- Searchable
- Auditable
- Recoverable

---

Responsibilities

The Work Resource is responsible for:

- Work Package creation
- Slot association
- Reel assignment
- Caption assignment
- Deadline management
- Screenshot collection
- Review status
- Work completion
- Work history reference

It does not manage:

- Worker identity
- Instagram account setup
- Training resources
- Weekly payment calculations

---

Ownership

Primary Owner:

Work Module

Only the Work Module may create or modify Work Resources.

---

Resource Lifetime

Property| Value
Created| Before scheduled slot
Delivered| At slot time
Updated| During submission & review
Archived| After completion
Deleted| Never (archive only)

---

Work Philosophy

Every scheduled slot creates one Work Resource.

Example:

09:00 Slot

↓

Work-1001

──────────

01:00 Slot

↓

Work-1002

──────────

08:00 Slot

↓

Work-1003

Each Work Resource is completely independent.

---

Work Identity

Every work assignment receives a permanent identifier.

Example:

WRK-000001

WRK-000002

WRK-000003

Rules:

- Never reused
- Never edited
- Never regenerated

---

Primary Fields

Every Work Resource should contain:

Field| Description
Work ID| Permanent identifier
Worker ID| Parent Worker
Season ID| Current season
Slot ID| Assigned slot
Work Status| Current state
Deadline| Completion deadline
Reel Package| Assigned reels
Caption Version| Assigned caption
Screenshot Status| Submission progress
Review Status| Review progress

---

Worker Relationship

Each Work Resource belongs to exactly one worker.

Worker

↓

Work Resource

A Work Resource cannot belong to multiple workers.

---

Slot Relationship

Every Work Resource belongs to exactly one scheduled slot.

Example:

09:00 Slot

↓

WRK-000125

Slot changes never modify completed Work Resources.

---

Work Package

A Work Package consists of:

- Assigned Reels
- Caption
- Upload Instructions
- Screenshot Requirement

Workers always receive a complete package.

---

Reel Package

The Work Resource stores references only.

Example:

WRK-001

↓

Reel-201

↓

Reel-205

↓

Reel-219

Actual video files remain in the Global Resource Library.

---

Caption Assignment

Stores:

- Caption Version Reference

Actual caption text belongs to the Global Resources.

---

Work Delivery

At slot time:

The system should:

1. Verify worker eligibility.
2. Verify account readiness.
3. Delete previous work reels from the chat.
4. Deliver the new Work Package.
5. Start the work timer.

This workflow should be automatic.

---

Previous Work Cleanup

Before sending a new Work Package:

The bot deletes the previous work package messages (reels, captions, related instructions) from the worker's chat.

Timeline and history remain unaffected.

This keeps the worker chat clean and reduces confusion.

---

Deadline Policy

Every Work Resource has one completion deadline.

Rule:

The worker must finish the work and submit all required screenshots before 30 minutes prior to the next scheduled slot.

Example:

09:00 Slot

↓

Next Slot

01:00 PM

↓

Submission Deadline

12:30 PM

After the deadline:

The Work Resource becomes Missed.

---

Work Status

Supported states:

- Scheduled
- Sent
- In Progress
- Submitted
- Under Review
- Approved
- Rejected
- Missed
- Cancelled

The current state is stored in the Work Resource.

History belongs to the Timeline Resource.

---

Current Scope

This part defines:

- Purpose
- Ownership
- Identity
- Work Package
- Slot Relationship
- Reel Assignment
- Caption Assignment
- Delivery
- Deadline
- Previous Work Cleanup
- Work States

The following parts will define:

- Screenshot Collection
- Review Queue
- Multi-Account Mapping
- Timeline
- Weekly Reward Integration
- Audit
- Migration
- Security
- Recovery
- Final Specification

---

End of Part 1

16_Work_Resource.md (Part 2)

«Document Version: 1.0
Status: In Progress
Module: Work Resource
Priority: Critical»

---

Work Execution Lifecycle

Every Work Resource follows a controlled lifecycle.

Created

↓

Scheduled

↓

Sent

↓

Worker Upload

↓

Screenshot Submission

↓

Review Queue

↓

Approved

OR

Rejected

OR

Missed

↓

Archived

Each transition creates a Timeline event.

---

Work Start

Work begins immediately after the Work Package is delivered.

There is no "Start Work" button.

The delivery of the work package automatically marks the work as In Progress.

This keeps the workflow simple and removes unnecessary user interaction.

---

Screenshot Submission

After uploading all assigned reels, the worker selects:

«Submit Work»

The bot then starts screenshot collection.

The worker never uploads screenshots before selecting Submit Work.

---

Screenshot Collection Philosophy

Screenshots are collected per Instagram account, not all at once.

This reduces confusion and allows administrators to review submissions more accurately.

---

Account-Based Screenshot Flow

Example:

Submit Work

↓

Account A Screenshot

↓

Accepted

↓

Account B Screenshot

↓

Accepted

↓

Account C Screenshot

↓

Submission Complete

The number of required screenshots is determined dynamically.

---

Dynamic Screenshot Count

The required screenshot count is always equal to the configured Instagram account count.

Examples:

1 Instagram Account

↓

1 Screenshot

────────────

2 Instagram Accounts

↓

2 Screenshots

────────────

3 Instagram Accounts

↓

3 Screenshots

No fixed limit exists inside the Work Resource.

---

Account Labels

Workers should always see friendly labels.

Example:

Please upload screenshot for:

Account A

After completion:

Now upload screenshot for:

Account B

Workers never see internal Instagram IDs.

---

Screenshot Mapping

Each screenshot is permanently mapped.

Example:

Account A

↓

Screenshot A

────────────

Account B

↓

Screenshot B

Mapping remains available during review.

---

Submission Rules

A Work Resource becomes Submitted only when:

- Every required screenshot is received.
- Every screenshot passes basic validation.
- The submission deadline has not expired.

Partial submissions remain In Progress.

---

Deadline Validation

Before accepting the final screenshot, the system checks:

Current Time

↓

Submission Deadline

↓

Valid?

↓

Accept

If the deadline has passed:

The Work Resource becomes Missed.

---

Missed Work Policy

A work assignment is considered missed when:

- The worker fails to submit all required screenshots before the deadline.
- The deadline is 30 minutes before the next scheduled slot.

Missed work:

- Cannot be submitted afterward.
- Remains visible in history.
- Affects weekly performance.

---

Review Queue

After successful submission:

Submitted

↓

Screenshot Review Queue

↓

Pending Review

The Review Module becomes responsible from this point.

---

Review Relationship

The Work Resource stores only:

- Review Status
- Review Reference

Review comments and decisions belong to the Review Resource.

---

Weekly Reward Integration

Every approved Work Resource contributes to the worker's weekly performance.

Examples:

- Completed Work Count
- Missed Work Count
- Approval Count

The Weekly Reward Module performs the final calculations.

The Work Resource only provides operational data.

---

Timeline Integration

The following actions create Timeline entries:

- Work Created
- Work Sent
- Screenshot Submitted
- Submission Completed
- Work Approved
- Work Rejected
- Work Missed

Timeline records are chronological and immutable.

---

Audit Integration

Administrative actions requiring audit:

- Force Approve
- Force Reject
- Manual Deadline Extension
- Manual Cancellation
- Manual Work Reassignment

Each audit record should include:

- Administrator
- Timestamp
- Worker ID
- Work ID
- Reason

---

Search Integration

Administrators should be able to search by:

- Work ID
- Worker ID
- Slot ID
- Season ID

Every search result should provide:

- Open Worker Profile
- Open Work Details
- Open Review
- View Timeline

---

Remaining Sections

The final part will define:

- Security Rules
- Recovery Policy
- Migration
- Health Checks
- Performance Guidelines
- Resource Diagram
- Field Classification
- Implementation Notes
- Final Specification

---

End of Part 2

16_Work_Resource.md (Part 3)

«Document Version: 1.0
Status: Approved
Module: Work Resource
Priority: Critical»

---

Security Rules

The Work Resource contains operational business data.

Access must follow the principle of least privilege.

Workers may:

- View current work.
- Submit screenshots.
- View work history.
- Check submission status.

Workers may not:

- View another worker's work.
- Edit submitted work.
- Modify deadlines.
- Change work status.
- Access internal review information.

---

Administrator Permissions

Action| Secondary Admin| Super Admin
View Work| ✅| ✅
Review Screenshots| Optional| ✅
Approve Work| Optional| ✅
Reject Work| Optional| ✅
Extend Deadline| Optional| ✅
Cancel Work| ❌| ✅
Delete Work| ❌| ❌

Completed Work Resources should never be permanently deleted.

---

Recovery Policy

If an operational error occurs before review:

Administrators may restore:

- Work Status
- Screenshot References
- Review Queue Position

Recovery should never duplicate work assignments.

---

Archive Policy

After completion, every Work Resource becomes part of the historical archive.

Archived work remains available for:

- Weekly Review
- Worker History
- Performance Reports
- Timeline
- Audit
- Migration

Archived work never becomes active again.

---

Migration Support

Migration preserves:

- Work ID
- Worker Reference
- Slot Reference
- Current Status
- Submission Status
- Screenshot References
- Review Status
- Timeline References

Work already completed before migration remains part of worker history.

---

Health Check Rules

The Health Checker should verify:

- Worker reference exists.
- Slot reference exists.
- Reel package exists.
- Caption reference exists.
- Screenshot mapping is complete.
- Review reference exists (when applicable).
- Deadline consistency.
- Valid work state.

Problems should be reported to administrators.

Automatic repair requires approval.

---

Resource Integrity Rules

Every Work Resource must satisfy:

✓ Existing Worker

✓ Existing Slot

✓ Existing Reel Package

✓ Existing Caption Version

✓ Valid Deadline

✓ Valid State

✓ Valid Screenshot Mapping

Broken operational data is not permitted.

---

Performance Guidelines

The Work Resource should never store:

- Reel video files
- Caption text
- Screenshot image files
- Review comments
- Notification history

Instead, it stores references to these resources.

This reduces duplication and improves scalability.

---

Search Optimization

Supported search methods:

- Work ID
- Worker ID
- Slot ID
- Season ID
- Review ID (through relationship)

Search results should provide:

- Worker Profile
- Work Details
- Screenshot Review
- Timeline
- Weekly Summary

---

Resource Relationships

Worker Resource
        │
        ▼
Work Resource
        │
        ├── Slot Resource
        ├── Reel Package Resource
        ├── Caption Resource
        ├── Screenshot Resource
        ├── Review Resource
        ├── Timeline
        └── Weekly Reward Resource

The Work Resource coordinates operational execution while specialized resources manage their own data.

---

Field Classification

The Work Resource contains three logical groups.

Identity

- Work ID
- Worker Reference
- Slot Reference
- Season Reference

---

Current Configuration

- Work Status
- Deadline
- Reel Package Reference
- Caption Version
- Screenshot Status
- Review Status

---

Metadata

- Created Date
- Sent Date
- Submission Date
- Review Date
- Last Updated

Historical events remain in the Timeline Resource.

---

Automation Integration

The Automation Engine interacts with the Work Resource for:

- Work creation
- Scheduled delivery
- Previous work cleanup
- Deadline monitoring
- Missed work detection
- Reminder notifications
- Archive processing

Automation never changes work without validation.

---

Worker Dashboard Integration

The Dashboard displays data from the current Work Resource.

Examples:

- Current Assignment
- Remaining Time
- Submission Status
- Next Slot
- Work History Shortcut

The Dashboard should never duplicate Work Resource data.

---

Future Expansion

The Work Resource is designed to support:

- Multiple work types
- Multiple campaigns
- AI-assisted review
- Priority work
- Quality scoring
- Bonus tasks
- Emergency assignments

Future capabilities should extend the resource without changing existing relationships.

---

Implementation Notes

Resource Type

Operational Resource

---

Primary Owner

Work Module

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

Work is immutable after archival.

Associated resources may be versioned independently.

---

Archive Supported

Yes

---

Recovery Supported

Yes

---

Cache Friendly

Yes

Only lightweight dashboard summaries should be cached.

---

Final Specification Summary

The Work Resource manages every scheduled work assignment within IWMS.

It controls:

- Work Package delivery
- Slot association
- Screenshot submission
- Review workflow
- Deadline enforcement
- Weekly reward contribution

while delegating media, reviews, and history to specialized resources.

This architecture provides:

- Predictable execution
- Strong auditability
- Clean separation of responsibilities
- High scalability
- Efficient automation
- Migration compatibility

---

Final Statement

The Work Resource is the official operational specification for daily work execution within IWMS.

All scheduling, work delivery, screenshot collection, review processing, and historical tracking must comply with this specification.

Any future feature affecting work execution must extend this architecture while maintaining compatibility with existing Worker, Slot, Review, and Timeline resources.

---

End of 16_Work_Resource.md
