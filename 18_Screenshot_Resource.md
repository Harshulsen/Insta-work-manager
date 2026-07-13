18_Screenshot_Resource.md

«Document Version: 1.0
Status: Approved
Module: Screenshot Resource
Priority: Critical»

---

Purpose

The Screenshot Resource manages every screenshot submitted by workers as proof of completed work.

Screenshots serve as the primary evidence for work verification before administrative review.

This resource is responsible for collecting, validating, storing, mapping, archiving, and presenting screenshots throughout their lifecycle.

---

Philosophy

Screenshots are evidence, not work.

A Work Resource represents the assigned task.

A Screenshot Resource represents the proof that the task was completed.

Every screenshot must always belong to exactly one Work Resource.

---

Responsibilities

The Screenshot Resource manages:

- Screenshot collection
- Screenshot validation
- Account mapping
- Submission order
- Review references
- Archive management
- Search support
- Timeline integration
- Audit support
- Migration support

It does not manage:

- Work generation
- Review decisions
- Rewards
- Worker identity

---

Ownership

Primary Owner:

Screenshot Module

---

Resource Lifetime

Property| Value
Created| During work submission
Updated| During validation
Reviewed| During admin review
Archived| After review
Deleted| Never (except retention policy)

---

Screenshot Philosophy

One screenshot belongs to one Instagram account.

One Instagram account belongs to one Work Resource.

Example:

Work WRK-10452

│

├── Account A → Screenshot 1

├── Account B → Screenshot 2

└── Account C → Screenshot 3

---

Screenshot Identity

Each screenshot receives its own permanent identifier.

Example:

SS-000001

SS-000002

SS-000003

Screenshot IDs never change.

---

Primary Fields

Field| Description
Screenshot ID| Permanent identifier
Work ID| Parent Work
Worker ID| Parent Worker
Instagram Account Slot| Account A / B / C
Screenshot Status| Current state
Upload Time| Timestamp
Review Status| Current review state
Screenshot File Reference| Media reference

---

Screenshot States

Supported states:

- Waiting
- Uploaded
- Validated
- Under Review
- Approved
- Rejected
- Archived

Current state is stored inside the Screenshot Resource.

---

Screenshot Collection

Screenshot collection begins only after:

Worker selects:

«Submit Work»

The bot then requests screenshots sequentially.

---

Upload Sequence

Example:

Submit Work

↓

Upload Account A

↓

Accepted

↓

Upload Account B

↓

Accepted

↓

Upload Account C

↓

Accepted

↓

Submission Complete

Sequence cannot be skipped.

---

Account Mapping

Every screenshot permanently maps to an account slot.

Example:

Account A

↓

SS-001

────────────

Account B

↓

SS-002

────────────

Account C

↓

SS-003

Workers never see internal Instagram IDs.

---

Validation Rules

Each screenshot must satisfy:

- Uploaded before deadline
- Valid image format
- Successfully received
- Correct upload order
- Correct account mapping

If validation fails:

The worker is asked to upload again.

---

Submission Completion

Submission completes only when:

- Every required screenshot is uploaded.
- Validation succeeds.
- Deadline has not expired.

Only then:

Work Status

↓

Submitted

---

Deadline Integration

The Screenshot Resource follows the deadline defined by the Slot Resource.

It never calculates deadlines independently.

---

Review Relationship

After successful submission:

Screenshot Resource

↓

Review Queue

↓

Review Resource

The Screenshot Resource stores only the Review Reference.

---

Review Status

Possible values:

- Pending
- Reviewing
- Approved
- Rejected

Detailed review notes belong to the Review Resource.

---

Timeline Integration

Timeline events include:

- Screenshot Upload Started
- Screenshot Uploaded
- Validation Passed
- Validation Failed
- Submission Completed
- Screenshot Approved
- Screenshot Rejected

---

Audit Integration

Administrative actions requiring audit:

- Manual Screenshot Removal
- Manual Screenshot Replacement
- Force Validation
- Force Approval

Audit records include:

- Administrator
- Worker
- Screenshot ID
- Work ID
- Timestamp
- Reason

---

Search Support

Search by:

- Screenshot ID
- Work ID
- Worker ID
- Account Slot

Results should allow:

- Open Worker Profile
- Open Work
- Open Review
- Open Timeline

---

Security Rules

Workers may:

- Upload screenshots.
- View uploaded screenshots before submission.
- Retry failed uploads.

Workers may not:

- Modify submitted screenshots.
- Replace screenshots after submission.
- Delete screenshots.

---

Administrator Permissions

Action| Secondary Admin| Super Admin
View Screenshot| ✅| ✅
Review Screenshot| Optional| ✅
Replace Screenshot| ❌| ✅
Delete Screenshot| ❌| ❌

---

Archive Policy

After review:

Screenshots move to archive.

Archived screenshots remain available for:

- Review History
- Timeline
- Worker History
- Audit
- Migration

---

Backup Policy

Backups preserve:

- Screenshot Metadata
- Work References
- Review References
- Media References

Image files should be backed up separately.

---

Health Check

The Health Checker verifies:

- Existing Work
- Existing Worker
- Valid Screenshot Mapping
- Missing Screenshot Files
- Broken References
- Invalid States

---

Performance Guidelines

The Screenshot Resource stores:

- Metadata
- References
- Status

It should not duplicate:

- Worker Information
- Work Information
- Review Notes

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
        ├── Review Resource
        ├── Timeline
        └── Audit

---

Field Classification

Identity

- Screenshot ID
- Work ID
- Worker ID

---

Current Configuration

- Account Slot
- Upload Status
- Review Status

---

Metadata

- Upload Time
- Validation Time
- Review Time

---

Future Expansion

Supports future features:

- AI Screenshot Validation
- OCR Verification
- Duplicate Detection
- Quality Score
- Auto Approval
- Batch Review

---

Database Schema Summary

Screenshot

│

├── Screenshot ID

├── Work ID

├── Worker ID

├── Account Slot

├── File Reference

├── Upload Time

├── Status

├── Review Reference

└── Timeline Reference

---

Edge Cases

- Worker uploads the wrong account screenshot.
- Worker uploads the same screenshot twice.
- Upload interrupted by Telegram.
- Deadline expires during upload.
- Administrator reopens review.
- Screenshot file becomes unavailable.
- Worker has only one configured Instagram account.
- Administrator changes Instagram account count after work assignment (existing work should continue with the original requirement).

---

Validation Checklist

Before accepting a screenshot:

- Worker exists.
- Work exists.
- Work is active.
- Screenshot deadline valid.
- Correct account slot requested.
- Valid image received.
- Upload sequence correct.

---

Implementation Checklist

- Screenshot ID generation
- Sequential upload flow
- Dynamic account count
- Account-slot mapping
- Validation pipeline
- Review queue integration
- Timeline creation
- Audit logging
- Archive handling
- Backup compatibility

---

TPY Implementation Notes

- Store only Telegram "file_id" (or equivalent media reference) in the resource.
- Account labels (Account A/B/C) should be generated dynamically.
- Required screenshot count must always come from the worker's configured Instagram account count.
- The upload handler must keep temporary session state until all screenshots are received or the process expires.

---

Final Statement

The Screenshot Resource is the official specification for proof-of-work management within IWMS.

Every work submission, screenshot upload, validation, review, archive, and audit process must follow this architecture.

Future enhancements should extend this specification while maintaining compatibility with the Work Resource, Review Resource, and Worker Resource.

---

End of 18_Screenshot_Resource.md
