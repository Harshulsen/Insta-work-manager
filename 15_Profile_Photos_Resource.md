15_Profile_Photos_Resource.md (Part 1)

«Document Version: 1.0
Status: In Progress
Module: Profile Photos Resource
Priority: Critical»

---

Purpose

The Profile Photos Resource manages every profile photo assigned to workers for their Instagram accounts.

Its purpose is to ensure that profile photos remain:

- Organized
- Version controlled
- Randomly assignable
- Reusable
- Trackable
- Consistent throughout the worker's lifecycle

This resource guarantees that every worker always receives the correct profile photos whenever they reopen the Training Center.

---

Philosophy

Profile photos are platform assets, not worker assets.

Workers receive temporary assignments.

Administrators always control:

- Available photo library
- Assignment rules
- Version updates
- Replacement decisions

Workers never permanently own profile photos.

---

Responsibilities

The Profile Photos Resource is responsible for:

- Managing the global photo library
- Creating profile photo packs
- Assigning packs to workers
- Version management
- Random assignment
- Preventing unnecessary duplication
- Maintaining assignment history
- Supporting account replacement
- Supporting migration

It does not manage:

- Instagram accounts
- Training videos
- Invite links
- Timeline history

---

Ownership

Primary Owner:

Profile Photos Module

Only this module may modify photo assignments.

---

Resource Lifetime

Property| Value
Created| By administrator
Assigned| During onboarding or reassignment
Updated| When a new pack is assigned
Archived| When retired
Deleted| Never directly (archive instead)

---

Resource Philosophy

There are two different concepts.

Photo Library

Stores every available photo.

Example:

PHOTO-001

PHOTO-002

PHOTO-003

PHOTO-004

PHOTO-005

---

Photo Pack

Groups multiple photos together.

Example:

Pack V1

├── PHOTO-001

└── PHOTO-002

Workers are assigned packs, not individual photos.

---

Photo Pack Rules

The number of photos inside a pack must always equal the configured number of Instagram accounts.

Examples:

1 Instagram Account

↓

1 Profile Photo

---

2 Instagram Accounts

↓

2 Profile Photos

---

3 Instagram Accounts

↓

3 Profile Photos

The system should reject incomplete packs.

---

Assignment Rules

During onboarding:

1. Determine required Instagram account count.
2. Select a compatible Photo Pack.
3. Assign the pack.
4. Store only the pack reference in the Worker Resource.

The image files remain in the Profile Photos Resource.

---

Random Assignment

When assigning profile photos automatically:

The system should:

- Choose a valid pack.
- Avoid recently overused packs (optional future enhancement).
- Record the assignment.
- Prevent duplicate references within the same worker.

Randomization should occur only during assignment.

It should never change automatically afterward.

---

Current Assignment

Every worker has exactly one active Profile Photo Pack.

Example:

Worker WK-154

↓

Photo Pack

↓

PACK-V3

The Worker Resource stores only the reference.

---

Pack Versioning

Photo Packs support versioning.

Example:

PACK-V1

↓

PACK-V2

↓

PACK-V3

Each version is immutable after publication.

---

Individual Photo Identity

Every photo receives a permanent identifier.

Example:

PHOTO-001

PHOTO-002

PHOTO-003

Photo IDs never change.

---

Search Support

Administrators should be able to search by:

- Pack ID
- Photo ID
- Worker ID

Search results should allow navigation to:

- Assigned Worker
- Pack Details
- Assignment History

---

Validation Rules

Every Photo Pack must satisfy:

- Correct number of photos.
- Existing photo references.
- No duplicate photos within the same pack.
- Valid version.
- Active status.

Invalid packs cannot be assigned.

---

Current Scope

This part defines:

- Purpose
- Ownership
- Photo Library
- Photo Packs
- Random Assignment
- Versioning
- Search
- Validation

The following parts will define:

- Assignment History
- Replacement Behaviour
- Timeline Integration
- Migration
- Audit
- Security
- Health Checks
- Recovery
- Implementation Notes
- Complete Resource Diagram

---

End of Part 1

15_Profile_Photos_Resource.md (Part 2)

«Document Version: 1.0
Status: In Progress
Module: Profile Photos Resource
Priority: Critical»

---

Assignment Lifecycle

Every Profile Photo Pack follows a defined assignment lifecycle.

Created

↓

Approved

↓

Available

↓

Assigned

↓

Active

↓

Reassigned (Optional)

↓

Archived

Only Approved packs may be assigned to workers.

---

Assignment History

Every assignment must be recorded.

History should include:

- Worker ID
- Pack ID
- Pack Version
- Assignment Date
- Assigned By
- Replacement Reason (if applicable)
- Unassigned Date

History is append-only.

Assignments must never be overwritten.

---

Assignment Philosophy

A worker should always receive the same assigned photos until an administrator intentionally changes them.

Opening the Training Center must never trigger a new random assignment.

Randomization occurs only once during assignment.

---

Worker Experience

Whenever the worker opens the Training Center:

The system should load:

Worker

↓

Assigned Pack Reference

↓

Profile Photos Resource

↓

Display Assigned Photos

The worker always sees the same profile photos unless the assignment has changed.

---

Account Mapping

Profile photos should always correspond to Instagram account slots.

Example:

Account A

↓

PHOTO-001

────────────

Account B

↓

PHOTO-002

────────────

Account C

↓

PHOTO-003

This mapping prevents confusion during account setup and screenshot submission.

---

Account Count Validation

Before assigning a Photo Pack:

The system verifies:

Required Instagram Accounts

↓

Configured Photo Count

↓

Equal?

↓

Assign

If the counts do not match:

Assignment is rejected.

---

Replacement Behaviour

When an Instagram account is replaced, administrators choose one of the following:

Option 1 — Keep Current Pack

The assigned Profile Photo Pack remains unchanged.

No new assignment is created.

---

Option 2 — Assign New Pack

The current assignment is archived.

A new Profile Photo Pack is assigned.

Timeline entries are generated.

---

Administrative Assignment

Administrators may manually assign:

- Any active Photo Pack
- Any compatible Photo Pack Version

Manual assignments require:

- Validation
- Timeline entry
- Audit record

---

Pack Retirement

Administrators may retire old packs.

Retired packs:

- Cannot be assigned to new workers.
- Continue working for already assigned workers until changed.
- Remain available for history and migration.

---

Pack Update Policy

A published pack is immutable.

If changes are required:

Create:

PACK-V3

↓

PACK-V4

Never modify an existing published version.

---

Timeline Integration

The following events create Timeline entries:

- Photo Pack Assigned
- Photo Pack Replaced
- Photo Pack Restored
- Photo Pack Updated
- Manual Assignment
- Assignment Removed

Timeline should reference:

- Worker ID
- Pack ID
- Pack Version

---

Audit Integration

Administrative actions requiring audit:

- Manual Pack Assignment
- Forced Replacement
- Pack Restoration
- Pack Retirement
- Assignment Override

Audit records should include:

- Administrator
- Timestamp
- Worker ID
- Pack Version
- Reason

---

Training Integration

The Training Resource references the assigned Photo Pack.

Whenever the worker reopens the Training Center:

The Training Resource loads:

Worker

↓

Training Assignment

↓

Photo Pack Reference

↓

Profile Photos Resource

↓

Display Photos

No duplicate images are stored inside the Training Resource.

---

Resource Relationships

Worker Resource

↓

Training Resource

↓

Profile Photos Resource

↓

Photo Library

The Worker Resource stores only the assigned Pack reference.

---

Migration Support

Migration preserves:

- Assigned Pack
- Pack Version
- Account Mapping
- Assignment History

Workers should continue seeing the same assigned photos after migration.

---

Remaining Sections

The final part will define:

- Security Rules
- Health Checks
- Recovery Policy
- Performance Guidelines
- Resource Diagram
- Field Classification
- Future Expansion
- Implementation Notes
- Final Specification

---

End of Part 2

15_Profile_Photos_Resource.md (Part 3)

«Document Version: 1.0
Status: Approved
Module: Profile Photos Resource
Priority: Critical»

---

Security Rules

Profile Photos are controlled platform resources.

Workers may:

- View assigned profile photos.
- Reopen assigned photos through the Training Center.

Workers may not:

- Browse the complete photo library.
- View unassigned packs.
- Download administrative metadata.
- Request random reassignment directly.

Only administrators may manage the Photo Library.

---

Administrator Permissions

Action| Secondary Admin| Super Admin
View Pack| ✅| ✅
Assign Pack| Optional| ✅
Replace Pack| Optional| ✅
Retire Pack| ❌| ✅
Restore Pack| Optional| ✅
Upload New Pack| Optional| ✅
Delete Pack| ❌| ❌

Profile Photo Packs should never be permanently deleted.

---

Health Check Rules

The Health Checker should verify:

- Assigned Pack exists.
- Pack contains the required number of photos.
- Every Photo ID exists.
- Worker reference exists.
- Account mapping is complete.
- Pack version is valid.

Problems should be reported to administrators.

Automatic correction should require approval.

---

Resource Integrity Rules

Every active assignment must satisfy:

✓ Existing Worker

✓ Existing Photo Pack

✓ Existing Photo IDs

✓ Valid Pack Version

✓ Correct Account Count

✓ Valid Status

Broken assignments are not allowed.

---

Recovery Policy

If a pack assignment is accidentally changed:

Administrators may restore the previous assignment.

Recovery restores:

- Pack Reference
- Pack Version
- Account Mapping

The recovery process should not create duplicate assignments.

---

Archive Policy

Archived Photo Packs remain available for:

- Timeline
- Audit
- Historical Training Preview
- Migration
- Worker History

Archived packs cannot be assigned to new workers.

---

Backup Policy

Backups should preserve:

- Photo Library
- Photo Packs
- Assignment History
- Worker References
- Pack Versions

Image files should be backed up separately from metadata whenever possible.

---

Performance Guidelines

The Profile Photos Resource should never duplicate:

- Worker information
- Training information
- Instagram information

It stores only:

- Photo metadata
- Pack definitions
- Assignment references

Large image files remain in the Global Media Library.

---

Search Optimization

Supported search methods:

- Worker ID
- Pack ID
- Photo ID
- Pack Version

Every search result should allow navigation to:

- Worker Profile
- Pack Details
- Assignment History

---

Resource Relationships

Worker Resource
        │
        ▼
Training Resource
        │
        ▼
Profile Photos Resource
        │
        ├── Photo Packs
        ├── Photo Library
        ├── Assignment History
        ├── Timeline
        └── Audit

The Training Resource consumes the assignment.

The Profile Photos Resource owns it.

---

Field Classification

The resource contains three logical groups.

Identity

- Pack ID
- Pack Version

---

Current Configuration

- Assigned Worker
- Assigned Photos
- Account Mapping
- Current Status

---

Metadata

- Created Date
- Assigned Date
- Last Updated
- Last Verified
- Replacement Count

Historical records remain in Assignment History.

---

Future Expansion

The architecture supports future additions.

Examples:

- Campaign-specific Photo Packs
- AI Quality Rating
- Face Similarity Detection
- Region-specific Packs
- Seasonal Packs
- Auto Rotation Policies
- Pack Usage Analytics

Future capabilities should extend the existing architecture without redesign.

---

Implementation Notes

Resource Type

Operational Resource

---

Primary Owner

Profile Photos Module

---

Parent Resource

Training Resource

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

Yes

Photo Packs are versioned.

Individual Photo IDs remain permanent.

---

Archive Supported

Yes

---

Recovery Supported

Yes

---

Cache Friendly

Yes

Only the currently assigned Pack reference should be cached.

---

Final Specification Summary

The Profile Photos Resource manages all profile photo assignments throughout the worker lifecycle.

It separates:

- Global Photo Library
- Versioned Photo Packs
- Worker Assignments
- Assignment History

This architecture guarantees:

- Consistent worker experience
- Random assignment only once
- Version control
- Historical traceability
- Easy migration
- Efficient storage
- Administrative flexibility

Workers always receive the same assigned profile photos until an administrator intentionally changes their assignment.

---

Final Statement

The Profile Photos Resource is the official specification for profile photo management within IWMS.

Every onboarding process, account replacement, training assignment, migration, and administrative workflow must follow the architecture defined in this document.

Any future enhancement related to profile photo management must extend this specification while maintaining compatibility with existing assignments and historical records.

---

End of 15_Profile_Photos_Resource.md
