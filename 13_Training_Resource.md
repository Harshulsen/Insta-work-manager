13_Training_Resource.md (Part 1)

«Document Version: 1.0
Status: In Progress
Module: Training Resource
Priority: Critical»

---

Purpose

The Training Resource manages every training-related asset, configuration, version, and assignment within the Instagram Workforce Management System (IWMS).

Its responsibility is not only to provide onboarding but also to ensure that every worker can always access the exact resources assigned to them, even months later.

The Training Resource guarantees consistency, repeatability, and version control.

---

Philosophy

Training is not an event.

Training is a permanent resource.

Every worker should always be able to reopen the Training Center and receive the correct resources according to their current assignment.

---

Objectives

The Training Resource should:

- Manage onboarding materials.
- Assign worker-specific resources.
- Manage global resources.
- Support versioning.
- Preserve historical snapshots.
- Support account replacement.
- Support migration.
- Support future expansion.

---

Resource Ownership

Primary Owner:

Training Module

Only the Training Module may modify training assignments.

Other modules reference training data but do not own it.

---

Resource Categories

Training resources are divided into two categories.

---

Global Resources

Resources shared by every worker.

Examples:

- Account Setup Video
- Upload Tutorial
- Bio Text
- Upload Instructions
- Audio Guide

Whenever administrators update these resources, every worker receives the latest approved version automatically.

---

Worker Resources

Resources assigned individually.

Examples:

- Telegram Invite Link
- Profile Photo Pack
- Instagram Account References
- Assigned Training Version

These resources remain fixed for the worker until an administrator changes them.

---

Resource Hierarchy

Training Resource

│

├── Global Resources

│     ├── Setup Video
│     ├── Upload Tutorial
│     ├── Audio Guide
│     ├── Bio Template
│     └── General Instructions

│

└── Worker Resources

      ├── Invite Link Reference
      ├── Profile Photo References
      ├── Instagram References
      ├── Assigned Training Version
      └── Training Snapshot

---

Training Assignment

Every worker receives one active training assignment.

The assignment contains references only.

Example:

Worker

↓

Training Assignment

↓

Global Resources

+

Worker Resources

The Training Resource never duplicates files unnecessarily.

---

Global Resource Rules

Global resources have these properties:

- Shared by all workers.
- Updated centrally.
- Version controlled.
- Automatically reflected in the Training Center.

Examples:

Setup Video v2

↓

All workers now see v2.

No manual reassignment required.

---

Worker Resource Rules

Worker resources have these properties:

- Individually assigned.
- Persist until changed.
- Version referenced.
- Never replaced automatically.

Example:

Worker WK-154

↓

Assigned Profile Photo Pack

↓

PHOTO-V3

The worker always receives PHOTO-V3 until an administrator assigns another version.

---

Training Version

Every worker has one current Training Version.

Example:

TRN-V1

TRN-V2

TRN-V3

A Training Version represents the complete training configuration assigned to the worker.

It is not limited to videos.

It also includes worker-specific references.

---

Training Package

A Training Package consists of:

- Setup Video Version
- Upload Tutorial Version
- Audio Version
- Bio Version
- Invite Link Reference
- Profile Photo Pack Reference

The package represents the worker's complete setup configuration.

---

Training Center

The Training Center is a permanent section inside the worker interface.

Workers may reopen it at any time.

Whenever opened, it should display:

- Current Global Resources
- Current Worker Resources

Historical versions are never shown unless explicitly requested by an administrator.

---

Current Scope

This part defines:

- Purpose
- Ownership
- Global Resources
- Worker Resources
- Training Versions
- Training Packages
- Training Center

The following parts will define:

- Training Snapshots
- Version Management
- Account Replacement Behaviour
- Resource Updates
- Timeline Integration
- Migration
- Validation
- Security
- Audit
- Implementation Notes
- Complete Resource Diagram

---

End of Part 1

13_Training_Resource.md (Part 2)

«Document Version: 1.0
Status: In Progress
Module: Training Resource
Priority: Critical»

---

Training Snapshot

A Training Snapshot preserves the exact training configuration assigned to a worker before major changes occur.

A snapshot is immutable.

Once created, it is never modified.

---

Snapshot Purpose

Snapshots allow administrators to answer:

- What training did this worker receive?
- Which profile photos were assigned?
- Which invite link was assigned?
- Which setup video was active?
- Which bio version was used?

This information remains available even after future updates.

---

Snapshot Creation Rules

A snapshot should be created before:

- Training Version changes
- Invite Link changes
- Profile Photo changes
- Bio changes
- Major account setup changes

Routine access to the Training Center should not create snapshots.

---

Snapshot Contents

Every Training Snapshot contains references to:

- Setup Video Version
- Upload Tutorial Version
- Audio Version
- Bio Version
- Invite Link Version
- Profile Photo Pack Version
- Instagram Account References
- Training Version
- Snapshot Timestamp

Media files themselves are not duplicated.

Only references are stored.

---

Version Management

Training supports versioning.

Example:

Training V1

↓

Training V2

↓

Training V3

Each version represents a complete training package.

Older versions remain available for administrative review.

---

Version Rules

Every Training Version:

- Has a unique identifier.
- Has a creation date.
- Has a creator.
- Has a change summary.
- References resource versions.
- May become inactive but is never modified after release.

---

Resource Update Policy

Training resources follow different update rules.

Global Resources

Examples:

- Setup Video
- Upload Tutorial
- Audio
- Bio Template

Rule:

Workers always receive the latest approved version.

---

Worker Resources

Examples:

- Invite Link
- Profile Photos
- Assigned Instagram Accounts

Rule:

Workers continue receiving the originally assigned resources until an administrator changes them.

---

Account Replacement Behaviour

Replacing an Instagram account does not automatically reset training.

Instead, administrators choose one of the following:

Option 1

Keep everything.

Only replace the Instagram account.

---

Option 2

Replace account and assign new profile photos.

---

Option 3

Replace account and generate a new invite link.

---

Option 4

Replace account and assign a completely new training package.

Every option creates Timeline entries.

---

Training Reassignment

Administrators may manually reassign training.

Example reasons:

- Major setup update
- Worker mistakes
- Campaign changes
- New onboarding process

Reassignment creates:

- New Training Version
- New Snapshot
- Timeline Entry

---

Training Center Behaviour

Whenever a worker opens the Training Center:

The system loads:

Current Global Resources

+ 

Current Worker Resources

The worker should always see the latest valid configuration.

Historical training packages remain hidden.

---

Administrative Preview

Administrators should be able to preview the exact training assigned to any worker.

The preview should display:

- Setup Video Version
- Upload Tutorial Version
- Audio Version
- Bio Version
- Invite Link
- Profile Photos
- Training Version

This preview should represent the worker's assigned configuration at the selected point in time.

---

Historical Preview

Administrators should also be able to open any Training Snapshot.

The system temporarily reconstructs the historical training package using stored references.

After the preview expires:

- Temporary preview messages are automatically deleted according to system policy.
- Snapshot data remains preserved.

---

Validation Rules

Training assignments are valid only when:

- Worker exists.
- Assigned resources exist.
- Training Version exists.
- Resource references are valid.
- Snapshot references are valid.

Invalid assignments should never become active.

---

Timeline Integration

Training generates Timeline entries for:

- Training Assigned
- Training Updated
- Snapshot Created
- Invite Link Changed
- Profile Photos Changed
- Bio Changed
- Training Reassigned

Timeline remains append-only.

---

Audit Integration

Administrative actions requiring audit include:

- Force Training Assignment
- Manual Version Override
- Snapshot Restoration
- Training Package Replacement

Audit records should include:

- Administrator
- Timestamp
- Worker ID
- Training Version
- Reason

---

Migration Support

Migration should preserve:

- Current Training Version
- Worker-specific resource references
- Training Snapshots
- Current Training Status

Global resources should reference the latest compatible versions after migration, unless compatibility rules require preserving older versions.

---

Security Rules

Workers may:

- Open Training Center.
- View assigned resources.
- Replay tutorials.

Workers may not:

- View historical versions.
- Change assigned resources.
- Access snapshots.
- Edit training configuration.

---

Remaining Sections

The final part will define:

- Recovery Policy
- Search Integration
- Performance Guidelines
- Resource Diagram
- Field Classification
- Future Expansion
- Implementation Notes
- Final Specification

---

End of Part 2

13_Training_Resource.md (Part 3)

«Document Version: 1.0
Status: Approved
Module: Training Resource
Priority: Critical»

---

Recovery Policy

The Training Resource should always support recovery.

Recovery should restore:

- Current Training Version
- Worker Resource References
- Assigned Invite Link
- Assigned Profile Photo Pack
- Assigned Bio Version
- Training Status

Recovery should never create duplicate assignments.

---

Search Integration

Administrators should be able to locate training using:

- Worker ID
- Training Version
- Training Snapshot ID
- Invite Link ID
- Channel Short Code

Every successful search should allow navigation to the Worker Profile or Training Preview.

---

Resource Integrity

The Training Resource should verify:

- Existing Worker
- Existing Training Version
- Existing Global Resources
- Existing Worker Resources
- Valid Resource References

Broken references should be reported through the Health Checker.

---

Performance Guidelines

Training Resources should remain lightweight.

Never duplicate:

- Videos
- Images
- Audio
- Documents

Only references should be stored.

This minimizes storage usage and simplifies updates.

---

Resource Diagram

Training Resource

│

├── Worker Reference

├── Training Version

├── Global Resources
│
│   ├── Setup Video
│   ├── Upload Tutorial
│   ├── Audio
│   └── Bio
│
├── Worker Resources
│
│   ├── Invite Link
│   ├── Profile Photo Pack
│   └── Instagram References
│
├── Snapshot References
│
└── Training Status

---

Resource Relationships

Worker

↓

Training Resource

↓

Training Version

↓

Global Resources

↓

Worker Resources

↓

Snapshots

↓

Timeline

Training acts as the bridge between onboarding materials and the worker.

---

Field Classification

The Training Resource contains three categories of information.

Current Configuration

- Current Training Version
- Current Status
- Assigned Resource References

---

Snapshot References

- Current Snapshot
- Previous Snapshots

---

Metadata

- Created Date
- Last Updated
- Last Verified

Historical changes remain in Timeline and Snapshot Resources.

---

Training Completion Rules

Training is considered complete only when:

- All required setup steps are completed.
- Required screenshots are approved (if configured).
- Worker state changes to Active.

Completing training automatically enables work eligibility.

---

Training Reopen Rules

Workers may reopen the Training Center at any time.

The system must always display:

- Latest Global Resources
- Current Worker Resources

Workers should never accidentally receive another worker's assigned resources.

---

Administrative Actions

Supported actions include:

- Assign Training
- Reassign Training
- Update Global Resources
- Assign New Profile Photos
- Assign New Invite Link
- Force Setup Review
- Preview Current Training
- Preview Historical Snapshot

Every action generates Timeline entries where applicable.

---

Backup Policy

Every system backup should include:

- Training Versions
- Worker Assignments
- Snapshot References

Large media files should be backed up separately through the Global Resources system.

---

Future Expansion

The Training Resource is designed for future capabilities.

Examples:

- Interactive Lessons
- Quizzes
- Skill Certifications
- AI-Assisted Training
- Campaign-Specific Training
- Multi-Language Training Packs

These additions should extend existing structures without redesigning the resource.

---

Implementation Notes

Resource Type

Operational Resource

---

Primary Owner

Training Module

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

(selected administrative operations)

---

Migration Supported

Yes

---

Backup Required

Yes

---

Cache Friendly

Yes

Frequently accessed resource references may be cached.

---

Versioned

Indirectly

The Training Resource references versioned assets rather than storing versions internally.

---

Archive Supported

Yes

Snapshots provide historical preservation.

---

Recovery Supported

Yes

---

Final Specification Summary

The Training Resource manages every aspect of worker onboarding and ongoing training.

It separates:

- Shared resources
- Worker-specific resources
- Historical snapshots
- Current assignments

This architecture guarantees:

- Consistency
- Repeatability
- Easy updates
- Historical traceability
- Efficient storage
- Migration compatibility

---

Final Statement

The Training Resource is the official specification for onboarding and training within IWMS.

Every setup workflow, training assignment, resource update, account replacement process, and migration must comply with this specification.

Future enhancements should extend this architecture rather than replacing it.

---

End of 13_Training_Resource.md
