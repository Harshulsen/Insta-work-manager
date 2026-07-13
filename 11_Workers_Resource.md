11_Workers_Resource.md (Part 1)

«Document Version: 1.0
Status: In Progress
Module: Workers Resource
Priority: Critical»

---

Purpose

The Workers Resource is the most important resource in the Instagram Workforce Management System (IWMS).

Every worker interacting with the platform has exactly one Worker Resource.

This resource represents the worker's permanent identity inside the system.

Unlike Instagram accounts, channel links, profile photos, or work assignments, the Worker Resource is designed to exist for the entire lifetime of the worker.

It acts as the central reference point for almost every other resource in the platform.

---

Philosophy

A Worker is permanent.

Everything else connected to the worker may change.

Examples:

- Instagram Accounts
- Telegram Invite Links
- Profile Photos
- Training Versions
- Slots
- Weekly Rewards
- Current Work

These resources may change multiple times during the worker's lifetime.

The Worker Resource itself should remain stable.

---

Responsibilities

The Workers Resource is responsible for:

- Permanent Worker Identity
- Worker Status
- Worker Configuration
- References to all child resources
- Current operational state
- Worker statistics
- Search indexing
- Resource relationships

The Workers Resource is not responsible for storing the full details of Instagram accounts, works, training files, or notifications. It stores references to those resources.

---

Design Principles

The Workers Resource follows these principles:

- One Worker → One Permanent Record
- Never duplicate worker identities.
- Never overwrite historical information without preserving history.
- Store references instead of embedding unrelated resources.
- Keep current state lightweight.
- Store historical data in dedicated history resources.
- Every Worker Resource must remain migration compatible.

---

Ownership

Primary Owner:

Worker Module

Other modules may read or reference Worker data, but only the Worker Module owns and controls this resource.

---

Resource Lifetime

Property| Value
Created| During Registration
Updated| Throughout Worker Lifetime
Deleted| Only by Super Admin according to deletion policy
Archived| Audit Record Only (after permanent deletion)

---

Worker Identity

Every worker has one permanent identity.

Identity never changes.

Identity exists independently of:

- Instagram Accounts
- Telegram Invite Links
- Current Training
- Current Campaign
- Current Slots

Worker identity survives migrations.

---

Primary Identity Fields

Every Worker Resource must contain the following permanent identity fields.

Field| Description
Worker ID| Permanent business identifier
Telegram ID| Permanent Telegram identifier
Telegram Username| Current Telegram username
Display Name| Current Telegram display name
Registration Date| Date worker joined
Registration Version| System version at registration
Preferred Language| English / Hinglish
Current Status| Active worker state
Worker Level| Current performance level

Worker ID is the primary identifier used throughout the platform.

Telegram ID is used internally.

---

Worker ID Standard

Worker IDs are permanent.

Example:

WK-154
WK-6456
WK-12854

Rules:

- Never reused.
- Never edited.
- Never reassigned.
- Never regenerated.
- Used in every major resource relationship.

---

Worker Identity Rules

The following rules always apply.

- One Telegram account can own only one Worker Resource.
- One Worker Resource belongs to only one Telegram account.
- Worker IDs remain immutable.
- Worker identity survives migration.
- Worker identity survives account replacement.
- Worker identity survives invite link regeneration.
- Worker identity survives training updates.

---

Worker Status

Every worker has exactly one primary state.

Current supported states:

- New
- Applying
- Training
- Verification Pending
- Active
- Needs Update
- Vacation
- Suspended
- Appeal Pending
- Removed
- Deleted

The Worker Resource stores only the current state.

State history is stored in the Timeline Resource.

---

Worker Level

Worker Level represents long-term performance.

Examples:

- Bronze
- Silver
- Gold
- Platinum

Worker Level is independent from:

- Weekly Reward
- Current Season
- Current Work

Future levels may be introduced without modifying the Worker Resource structure.

---

Registration Information

The Worker Resource records the initial registration details.

Includes:

- Registration Date
- Registration Source (future)
- Registration Version
- Initial Language
- Initial System Version

This information never changes after registration.

---

Search Index

The Worker Resource should expose searchable fields.

Supported search keys include:

- Worker ID
- Telegram ID
- Username
- Display Name
- Current Invite Link
- Current Channel Short Code
- Current Instagram Username(s)

Search should always resolve to the Worker Profile.

---

Relationships (Overview)

The Worker Resource is the parent resource for:

- Instagram Accounts
- Slots
- Training
- Works
- Notifications
- Timeline
- Weekly Rewards
- Support Tickets
- Bug Reports

These relationships are maintained through references rather than duplicated data.

---

Resource Rules

The Worker Resource must never contain:

- Reel files
- Screenshot files
- Training videos
- Large media
- Notification history
- Timeline history

Only references to these resources should be stored.

This keeps the Worker Resource lightweight and scalable.

---

Current Scope

This document currently defines:

- Purpose
- Ownership
- Identity
- Lifetime
- Status
- Worker ID
- Registration
- Search
- Relationships

The following sections will be completed in subsequent parts:

- Worker Configuration
- Resource References
- Statistics
- Validation Rules
- State Rules
- Migration
- Timeline Integration
- Audit Rules
- Security Rules
- Implementation Notes
- Complete Resource Diagram

---

End of Part 1

11_Workers_Resource.md (Part 2)

«Document Version: 1.0
Status: In Progress
Module: Workers Resource
Priority: Critical»

---

Worker Configuration

The Worker Resource stores the worker's current configuration.

Configuration represents the worker's present operational setup.

Historical configurations are stored separately in Timeline and Snapshot resources.

---

Configuration Philosophy

The Worker Resource should always answer one question:

«"If the worker opens the bot right now, what configuration should the system use?"»

Only the current configuration belongs here.

---

Configuration Groups

The Worker Resource stores references to the following configuration groups.

Worker Configuration

│

├── Language

├── Training

├── Instagram Accounts

├── Slots

├── Channel Link

├── Profile Photos

├── Current Season

├── Current Work

├── Dashboard

└── Permissions

Each group references another resource.

---

Language Configuration

Stores:

- Current Interface Language

Supported values:

- English
- Hinglish

Future languages can be added without changing the Worker Resource structure.

---

Training Reference

The Worker Resource never stores training files.

Instead it stores:

- Current Training Version
- Current Training Snapshot ID
- Training Status

Training details remain inside the Training Resource.

---

Instagram Reference

The Worker Resource stores references only.

Example:

Account A → IG-1025

Account B → IG-1026

Account C → IG-1027

The complete Instagram information exists inside the Instagram Resource.

---

Channel Link Reference

Stores:

- Current Invite Link ID
- Current Channel Short Code

Example:

Invite Link

↓

CH-01452

↓

Short Code

↓

GPA-WK154-V2

Old links are never stored here.

History belongs to the Link History Resource.

---

Profile Photo Reference

Stores:

- Assigned Profile Photo Pack Version
- Assigned Photo IDs

The Worker Resource never stores image files.

---

Slot Configuration

Stores:

- Daily Slot Count
- Preferred Slot Times
- Temporary Schedule Status
- Vacation Status

Work scheduling depends on this configuration.

---

Current Work Reference

Stores only:

- Active Work ID

Never stores:

- Reels
- Caption
- Screenshots

Those belong to the Work Resource.

---

Current Season

Stores:

- Current Season ID

Example:

Season

↓

S-2026-W28

Historical seasons remain inside the History Resource.

---

Dashboard Configuration

Stores references required to build the dashboard quickly.

Examples:

- Current Work
- Next Slot
- Reward Status
- Pending Notifications

Dashboard should be generated from references rather than duplicated data.

---

Notification Reference

Stores:

- Pending Notification Count
- Last Notification ID (optional)

Notification history belongs to the Notification Resource.

---

Support Reference

Stores:

- Current Open Ticket Count

Support conversations remain inside the Support Resource.

---

Bug Report Reference

Stores:

- Current Open Bug Count

Reports remain inside the Bug Report Resource.

---

Weekly Reward Reference

Stores only:

- Current Reward Status
- Current Season Reward ID

Payment history belongs to the Reward Resource.

---

Worker Statistics

The Worker Resource maintains lightweight statistics.

Examples:

- Total Work Assigned
- Total Work Approved
- Total Work Missed
- Total Seasons Completed
- Account Replacement Count
- Training Version Count

Large statistical calculations belong to the Analytics Module.

---

Derived Statistics

Some values should never be stored permanently.

Examples:

- Approval Percentage
- Weekly Completion Rate
- Current Rank

These should be calculated dynamically when required.

---

Validation Rules

Every update to the Worker Resource must satisfy:

1. Worker exists.
2. Worker is not deleted.
3. State transition is valid.
4. Permission check passes.
5. Related resources exist.
6. Resource ownership is valid.

Only then should updates be written.

---

Reference Validation

Every referenced object must exist.

Example:

Worker

↓

Instagram ID

↓

Instagram Resource Exists?

↓

Yes

↓

Save

Broken references are never allowed.

---

Dependency Rules

The Worker Resource depends on:

- Training Resource
- Instagram Resource
- Slot Resource
- Work Resource
- Timeline Resource
- Notification Resource

These dependencies are reference-based only.

---

Configuration Update Rules

Whenever configuration changes:

1. Validate request.
2. Create snapshot (if required).
3. Update related resource.
4. Update Worker reference.
5. Create timeline entry.
6. Notify worker (if required).

---

State Synchronization

Current worker state must remain synchronized with related resources.

Example:

Worker State:

Needs Update

↓

Work Assignment

↓

Blocked

↓

Notification Sent

No conflicting states should exist.

---

Cache Policy

The Worker Resource may cache lightweight information for faster access.

Allowed examples:

- Current dashboard summary
- Next slot time
- Pending work count

Heavy data must never be cached here.

---

Performance Principles

The Worker Resource should remain lightweight.

Avoid storing:

- Media
- Large histories
- Repeated information
- Duplicate statistics

Only current references and essential metadata belong here.

---

Implementation Notes (Part 2)

Worker Resource should:

- Reference, not duplicate.
- Store only current configuration.
- Keep historical data in dedicated resources.
- Validate every relationship before saving.
- Remain optimized for frequent reads.

---

Remaining Sections

The following sections will be completed in Part 3:

- Migration Rules
- Timeline Integration
- Audit Integration
- Security Rules
- Deletion Policy
- Recovery Policy
- Search Optimization
- Future Expansion
- Complete Worker Resource Diagram
- Final Specification

---

End of Part 2

11_Workers_Resource.md (Part 3)

«Document Version: 1.0
Status: In Progress
Module: Workers Resource
Priority: Critical»

---

Migration Rules

The Worker Resource is the primary resource used during system migration.

Migration must preserve:

- Worker ID
- Telegram ID
- Registration Information
- Current Status
- Worker Level
- Current Configuration
- Resource References

The worker should continue exactly from the previous state.

---

Migration Philosophy

Migration should feel invisible to the worker.

The worker should never repeat:

- Registration
- Training
- Setup
- Language Selection

unless explicitly required by an administrator.

---

Migration Package

A migration package should contain references only.

Example:

Worker

↓

Identity

↓

Configuration

↓

References

↓

Current State

↓

Current Season

Large historical data should migrate separately.

---

Timeline Integration

Every important Worker Resource update creates a Timeline entry.

Examples:

- Worker Registered
- Language Changed
- Training Assigned
- Training Updated
- Instagram Account Replaced
- Channel Link Changed
- Profile Photo Updated
- Vacation Started
- Vacation Ended
- Worker Removed
- Worker Restored

Timeline records are append-only.

---

Audit Integration

Certain actions require permanent audit records.

Examples:

- Worker Deleted
- Worker Restored
- Manual Status Change
- Manual Reward Override
- Permission Override

Each audit record should include:

- Action
- Performed By
- Timestamp
- Reason
- Related Worker ID

Audit records are immutable.

---

Security Rules

The Worker Resource contains sensitive operational data.

Access should follow the principle of least privilege.

Worker view:

- Only personal information.
- No internal references.
- No administrative metadata.

Secondary Admin:

- Only permitted fields.

Super Admin:

- Full access.

Developer Mode:

- Test environment only.

---

Data Visibility Matrix

Field| Worker| Secondary Admin| Super Admin
Worker ID| ✅| ✅| ✅
Telegram ID| ❌| Optional| ✅
Username| ✅| ✅| ✅
Status| ✅| ✅| ✅
Worker Level| ✅| ✅| ✅
Timeline| Partial| According to Permission| ✅
Audit Records| ❌| ❌| ✅
Internal References| ❌| ❌| ✅

Visibility should always be permission-controlled.

---

Deletion Policy

Deleting a worker is a high-risk operation.

Recommended flow:

Active Worker

↓

Removed

↓

Retention Period (Optional)

↓

Permanent Delete

↓

Minimal Audit Record Preserved

Deletion should require confirmation according to project policy.

---

Recovery Policy

Recovery is preferred over recreation.

If a worker is mistakenly removed:

Restore the Worker Resource.

Do not create a new Worker ID.

Recovery should preserve:

- Identity
- References
- Configuration
- Progress

---

Search Optimization

The Worker Resource is the central search target.

Search should support:

- Worker ID
- Telegram ID
- Username
- Display Name
- Instagram Username
- Channel Short Code
- Invite Link
- Support Ticket ID
- Bug Report ID
- Work ID

Whenever possible, search should resolve to the Worker Profile.

---

Resource Integrity Rules

The Worker Resource must never contain broken references.

Integrity checks should verify:

- Existing Instagram references
- Existing Training references
- Existing Work references
- Existing Slot references
- Existing Notification references

Invalid references should be detected by Health Check tools.

---

Health Check Integration

The Health Checker should validate:

- Missing references
- Invalid states
- Duplicate Worker IDs
- Orphaned child resources
- Configuration inconsistencies

Health checks should generate reports instead of modifying production data automatically.

---

Backup Integration

Every backup should include the Worker Resource.

Minimum backup contents:

- Identity
- Configuration
- References
- Current State

Historical resources may be backed up separately.

---

Resource Dependencies

The Worker Resource depends on:

- Instagram Resource
- Training Resource
- Slot Resource
- Work Resource
- Timeline Resource
- Notification Resource
- Weekly Reward Resource

These dependencies should remain loosely coupled through references.

---

Future Expansion

The Worker Resource is designed to support future features without structural redesign.

Examples:

- Multiple Campaign Membership
- Reputation Score
- Skill Levels
- Referral Information
- AI Quality Score
- External Verification
- Multi-Business Support

Future fields should be optional whenever possible.

---

Worker Resource Diagram

Worker Resource

│
├── Identity
│   ├── Worker ID
│   ├── Telegram ID
│   ├── Username
│   ├── Display Name
│   └── Registration Info
│
├── Status
│
├── Configuration
│   ├── Language
│   ├── Training Reference
│   ├── Instagram References
│   ├── Slot Reference
│   ├── Channel Link Reference
│   ├── Profile Photo Reference
│   └── Current Season
│
├── Statistics
│
├── Search Index
│
└── Resource References

---

Implementation Notes

Resource Type

Master Resource

---

Ownership

Worker Module

---

Lifetime

Permanent

---

Versioned

No

(Configuration references may point to versioned resources.)

---

Search Indexed

Yes

---

Timeline Enabled

Yes

---

Audit Enabled

Yes (selected operations)

---

Migration Supported

Yes

---

Backup Required

Yes

---

Cache Friendly

Yes

Only lightweight summary data should be cached.

---

Child Resources

- Instagram Accounts
- Slots
- Works
- Notifications
- Timeline
- Support Tickets
- Bug Reports
- Weekly Rewards

---

Parent Resource

System

---

Final Specification Summary

The Worker Resource serves as the permanent identity and central reference point for every worker in IWMS.

It does not own operational or historical business data directly.

Instead, it maintains the current configuration and references to specialized resources.

This design keeps the Worker Resource:

- Lightweight
- Scalable
- Searchable
- Migration-Friendly
- Maintainable
- Suitable for large-scale workforce management

---

Final Statement

The Worker Resource is the foundation of the IWMS data model.

Every major module in the platform ultimately relates back to this resource.

Any future change affecting worker identity, configuration, references, or lifecycle must update this specification before implementation.

---

End of 11_Workers_Resource.md
