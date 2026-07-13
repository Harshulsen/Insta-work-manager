12_Instagram_Accounts_Resource.md (Part 1)

«Document Version: 1.0
Status: In Progress
Module: Instagram Accounts Resource
Priority: Critical»

---

Purpose

The Instagram Accounts Resource manages every Instagram account assigned to workers within the Instagram Workforce Management System (IWMS).

Unlike the Worker Resource, which represents a permanent identity, the Instagram Accounts Resource manages temporary operational accounts that may be replaced multiple times during a worker's lifetime.

This resource is responsible for maintaining the current configuration, operational status, and historical continuity of every Instagram account.

---

Philosophy

A Worker is permanent.

An Instagram Account is replaceable.

Workers continue working even if their Instagram accounts change.

Therefore:

- Worker identity never changes.
- Instagram accounts may change at any time.
- The relationship between workers and Instagram accounts is dynamic.

---

Responsibilities

The Instagram Accounts Resource is responsible for:

- Instagram account registration
- Account verification
- Username management
- Profile setup status
- Bio verification
- Assigned profile photos
- Assigned Telegram invite link
- Account replacement
- Account lifecycle
- Account history references

This resource does not manage:

- Work assignments
- Weekly rewards
- Timeline history
- Training files

---

Ownership

Primary Owner:

Instagram Module

Only the Instagram Module may directly modify this resource.

Other modules interact through references.

---

Resource Lifetime

Property| Value
Created| During worker onboarding or account replacement
Updated| Whenever account configuration changes
Archived| After replacement
Deleted| Never directly (archived instead)

Historical accounts should remain available for auditing.

---

Resource Philosophy

Each Instagram account is an independent resource.

Example:

Worker WK-154

│

├── IG-1025 (Archived)

├── IG-1188 (Archived)

└── IG-1342 (Current)

The Worker Resource points only to the current active accounts.

---

Core Identity

Each Instagram account receives its own permanent identifier.

Example:

IG-1025

IG-1026

IG-2048

Instagram IDs never change.

---

Primary Fields

Every Instagram Account Resource should contain:

Field| Description
Instagram ID| Permanent identifier
Worker ID| Parent worker reference
Account Slot| Account A / B / C
Instagram Username| Current username
Instagram Profile Link| Current profile URL
Account Status| Current operational state
Setup Status| Current setup progress
Replacement Count| Number of replacements
Assigned Invite Link| Current Telegram invite link
Assigned Profile Photos| Current profile photo references

---

Worker Relationship

Each Instagram account belongs to exactly one worker.

Example:

Worker WK-154

↓

Account A

↓

IG-1025

Instagram accounts cannot belong to multiple workers simultaneously.

---

Account Slots

Each worker may have multiple account slots.

Example:

Account A

Account B

Account C

The number of slots is configurable by administrators.

Slots remain stable even when accounts are replaced.

Example:

Account A

↓

IG-1025

↓

Replaced

↓

IG-1188

↓

Replaced

↓

IG-1450

The slot remains Account A.

Only the assigned account changes.

---

Instagram Username

Stores the current Instagram username.

Username changes should be recorded through Timeline events.

Historical usernames belong to the History Resource.

---

Profile Link

Stores the current Instagram profile URL.

Validation rules:

- Must be a valid Instagram profile.
- Must not duplicate another active account (if configured).
- Must be reachable at the time of submission (when verification is enabled).

---

Account Status

Each account maintains its own independent state.

Supported states:

- Registered
- Pending Setup
- Ready
- Needs Update
- Replacement Requested
- Replaced
- Disabled

Worker state and account state remain independent.

---

Setup Status

Represents completion of required setup tasks.

Examples:

- Not Started
- In Progress
- Completed
- Verification Pending
- Requires Update

Only fully configured accounts become eligible for work.

---

Assigned Telegram Invite Link

Each Instagram account references the worker's current Telegram invite link.

The account never stores the invite link itself.

It stores only the reference.

Example:

IG-1025

↓

Channel Link Resource

↓

CH-01452

---

Assigned Profile Photos

Each account stores references to assigned profile photos.

Example:

Account A

↓

Photo Set

↓

PHOTO-001

Image files remain inside the Global Resources system.

---

Bio Configuration

Stores:

- Bio Version Reference
- Bio Setup Status

The actual bio text belongs to the Training Resource.

---

Replacement Count

Tracks how many times this account slot has been replaced.

Example:

Account A

↓

Replacement Count

↓

3

This value helps administrators identify unstable accounts.

---

Search Index

Supported search keys:

- Instagram ID
- Instagram Username
- Profile Link
- Worker ID
- Channel Short Code

Searching by an Instagram username should always resolve to the corresponding Worker Profile.

---

Validation Rules

Every Instagram account must satisfy:

- Valid profile link
- Assigned worker exists
- Slot exists
- Status is valid
- Required setup completed
- References are valid

Invalid accounts cannot become active.

---

Current Scope

This part defines:

- Purpose
- Ownership
- Identity
- Account Slots
- Core Fields
- Relationships
- Validation

The following parts will define:

- Account Replacement Workflow
- Versioning
- Timeline Integration
- Migration
- Security
- Audit
- Recovery
- Health Checks
- Implementation Notes
- Complete Resource Diagram

---

End of Part 1

12_Instagram_Accounts_Resource.md (Part 2)

«Document Version: 1.0
Status: In Progress
Module: Instagram Accounts Resource
Priority: Critical»

---

Account Lifecycle

Every Instagram account follows a defined lifecycle.

Account Submitted

↓

Validation

↓

Setup Required

↓

Verification

↓

Ready

↓

Working

↓

Needs Update (Optional)

↓

Replacement Requested (Optional)

↓

Replaced

↓

Archived

Every transition creates a Timeline event.

---

Account Replacement Philosophy

Instagram accounts are expected to change throughout a worker's lifetime.

Replacement is considered a normal business operation.

Replacing an account should never require:

- New Worker ID
- New Registration
- New Training (unless required)
- New Slot Configuration
- New Worker Profile

Only the affected account should change.

---

Replacement Reasons

Every replacement request should include a reason.

Supported reasons:

- Account Banned
- Login Issue
- Security Issue
- Shadow Ban
- Username Change
- Worker Request
- Admin Decision
- Other

Reason history should be preserved.

---

Replacement Workflow

Worker Request

↓

Validation

↓

Admin Review

↓

Approval

↓

Archive Old Account

↓

Create New Instagram Resource

↓

Assign To Same Slot

↓

Update Worker References

↓

Timeline

↓

Notification

↓

Continue Working

The worker should resume without restarting onboarding.

---

Slot Preservation Rule

Slots are permanent.

Accounts are temporary.

Example:

Account A

↓

IG-1025

↓

Replaced

↓

IG-1188

↓

Replaced

↓

IG-1450

The slot remains Account A.

---

Invite Link Handling

By default, the worker keeps the existing assigned Telegram invite link.

However, administrators may choose:

- Keep Existing Link
- Generate New Link
- Restore Previous Link

If a new link is assigned:

- Create a new Link Version.
- Preserve Link History.
- Update Worker Resource reference.

---

Profile Photo Handling

When replacing an account, administrators choose one of the following:

Option 1 — Keep Existing Photos

Assigned photo references remain unchanged.

---

Option 2 — Assign New Photo Pack

The system assigns a new profile photo version.

The previous assignment is preserved in history.

---

Bio Handling

Administrators choose:

- Keep Current Bio
- Apply Latest Global Bio
- Apply Custom Bio

Every change creates a Timeline entry.

---

Training Handling

Account replacement should not automatically restart training.

However, administrators may require:

- Setup Tutorial Review
- Upload Tutorial Review
- Full Setup Review

Training decisions remain configurable.

---

Setup Verification

After replacement, the worker must submit setup screenshots again.

The required screenshot count equals the configured Instagram account count.

Example:

Configured Accounts

↓

2

↓

Required Setup Screenshots

↓

2

Verification is completed before work resumes.

---

Work Assignment During Replacement

Workers with pending replacement should not receive new work.

Instead, the Dashboard displays a notice such as:

Account update required.

Please complete your account setup to continue receiving work.

After successful verification:

Work resumes automatically.

---

Account History

Every Instagram account should preserve:

- Username History
- Status History
- Replacement Reason
- Replacement Date
- Invite Link Version
- Profile Photo Version
- Bio Version

History should remain immutable.

---

Timeline Integration

The following events generate Timeline entries:

- Instagram Registered
- Setup Completed
- Setup Updated
- Replacement Requested
- Replacement Approved
- Replacement Completed
- Username Changed
- Invite Link Changed
- Profile Photos Updated
- Bio Updated

---

Audit Integration

Administrative actions requiring audit:

- Force Replacement
- Manual Username Edit
- Manual Status Override
- Replacement Cancellation
- Manual Link Assignment

Each audit record should include:

- Performed By
- Timestamp
- Reason
- Worker ID
- Instagram ID

---

Migration Support

Migration preserves:

- Current Instagram Accounts
- Slot Mapping
- Replacement Count
- Current Status
- Assigned Resources

Archived accounts should migrate separately if history migration is enabled.

---

Health Check Rules

Health Checker validates:

- Broken Worker Reference
- Invalid Slot
- Missing Invite Link
- Missing Photo Reference
- Invalid Account Status
- Duplicate Active Username (if restricted)

Problems are reported, not automatically corrected.

---

Security Rules

Workers can:

- View current account configuration.
- Request replacement.
- Submit updated accounts.

Workers cannot:

- Modify internal IDs.
- Access history.
- Change slot assignments.
- Edit administrative metadata.

---

Resource Relationships

Instagram Account

│

├── Worker Resource

├── Training Resource

├── Channel Link Resource

├── Profile Photo Resource

├── Timeline Resource

└── History Resource

The Instagram Resource owns only current account information.

---

Implementation Notes

Resource Type

Operational Resource

---

Owner

Instagram Module

---

Lifetime

Replaceable

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

Versioned

No

(Versioned resources are referenced instead.)

---

Backup Required

Yes

---

Child Resources

None

---

Parent Resource

Worker Resource

---

Remaining Sections

The final part will define:

- Deletion Policy
- Recovery Policy
- Performance Guidelines
- Resource Diagram
- Complete Field Matrix
- Future Expansion
- Final Specification

---

End of Part 2

12_Instagram_Accounts_Resource.md (Part 3)

«Document Version: 1.0
Status: Approved
Module: Instagram Accounts Resource
Priority: Critical»

---

Deletion Policy

Instagram accounts should almost never be permanently deleted.

Instead:

Active Account

↓

Replaced

↓

Archived

↓

History Preserved

Permanent deletion should only occur during worker deletion according to the platform's retention policy.

---

Archive Policy

Archived accounts remain available for:

- Timeline
- Audit
- Replacement History
- Analytics
- Migration (optional)

Archived accounts never receive new work.

---

Recovery Policy

If an administrator restores an archived account:

The system should verify:

- Username validity
- Invite Link assignment
- Profile setup
- Resource integrity

After verification:

The account may become active again.

---

Version Relationships

Instagram accounts reference versioned resources.

Examples:

- Invite Link Version
- Profile Photo Version
- Training Version
- Bio Version

The Instagram Resource itself is not versioned.

Only its linked resources are.

---

Current Resource References

Every active Instagram account maintains references to:

- Worker Resource
- Current Invite Link
- Current Profile Photo Pack
- Current Bio Version
- Current Training Version
- Current Slot

No duplicate information should be stored.

---

Data Integrity Rules

Every Instagram Resource must satisfy:

✓ Existing Worker

✓ Existing Slot

✓ Existing Invite Link

✓ Existing Profile Photos

✓ Valid Current State

✓ Valid Resource References

Broken references are prohibited.

---

Duplicate Rules

The system should prevent accidental duplicate assignments.

Examples:

Two workers

↓

Same active Instagram account

❌ Not Allowed

---

Same account

↓

Two active slots

❌ Not Allowed

---

Archived account

↓

Referenced as current

❌ Not Allowed

---

Performance Guidelines

The Instagram Resource should remain lightweight.

Never store:

- Uploaded screenshots
- Timeline history
- Review history
- Training videos
- Profile images
- Invite links directly

Only references belong here.

---

Search Optimization

Supported search methods:

- Instagram ID
- Username
- Worker ID
- Profile URL
- Channel Short Code

Future support:

- Historical Username Search
- Replacement History Search

Every successful search should resolve to the Worker Profile whenever applicable.

---

Resource Diagram

Instagram Resource

│

├── Identity
│
├── Worker Reference
│
├── Slot
│
├── Username
│
├── Profile Link
│
├── Current Status
│
├── Setup Status
│
├── Replacement Count
│
├── Invite Link Reference
│
├── Profile Photo Reference
│
├── Bio Version Reference
│
└── Training Version Reference

---

Resource Relationships

Worker

↓

Instagram Resource

↓

Invite Link Resource

↓

Profile Photo Resource

↓

Training Resource

↓

Timeline

↓

History

The Instagram Resource is the central operational resource for account management.

---

Field Classification

The resource contains three categories of fields.

Permanent Fields

- Instagram ID
- Worker Reference
- Slot

---

Current Configuration

- Username
- Profile URL
- Status
- Setup Status
- Current References

---

Operational Metadata

- Replacement Count
- Last Updated
- Last Verified

Historical information belongs to History Resources.

---

Maintenance Rules

Administrators may require:

- Username update
- Bio update
- Profile photo update
- Invite link update
- Complete setup refresh

During maintenance:

New work assignments should remain paused until verification is completed.

---

Administrator Actions

Supported administrative operations:

- Replace Account
- Update Username
- Change Status
- Assign New Link
- Restore Previous Link
- Assign New Profile Photos
- Force Verification
- Archive Account
- Restore Archived Account

Every operation should create Timeline entries.

---

Worker Actions

Workers may:

- Submit account
- Request replacement
- Update account (when requested)
- View assigned configuration
- Reopen Training Center

Workers may not:

- Change slot ownership
- Change internal references
- Modify history
- Edit administrative metadata

---

Future Expansion

The Instagram Resource should support future additions.

Examples:

- Multiple Campaign Accounts
- AI Verification
- Risk Score
- Quality Score
- Device Association
- Region Assignment
- Platform Expansion

These features should integrate without redesigning the resource.

---

Implementation Notes

Resource Type

Operational Resource

---

Primary Owner

Instagram Module

---

Parent Resource

Worker Resource

---

Child Resources

None

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

Cache Required

Minimal

Only lightweight metadata may be cached.

---

Versioned

No

Linked resources may be versioned independently.

---

Archive Supported

Yes

---

Recovery Supported

Yes

---

Final Specification Summary

The Instagram Accounts Resource manages every operational Instagram account used by workers.

It keeps only the current account configuration while delegating historical records, versioned resources, and media to specialized resources.

This design ensures:

- Simple replacements
- Strong auditability
- Lightweight storage
- Easy migration
- High scalability
- Clean separation of responsibilities

---

Final Statement

The Instagram Accounts Resource is the official specification for managing worker Instagram accounts in IWMS.

All onboarding, setup, verification, replacement, and maintenance workflows must comply with the architecture defined in this document.

Any future modification affecting Instagram account behavior must update this specification before implementation.

---

End of 12_Instagram_Accounts_Resource.md
