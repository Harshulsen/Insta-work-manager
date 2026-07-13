14_Channel_Link_Resource.md (Part 1)

«Document Version: 1.0
Status: In Progress
Module: Channel Link Resource
Priority: Critical»

---

Purpose

The Channel Link Resource manages every Telegram channel assigned to workers for use in Instagram bios, stories, highlights, and other required placements.

Unlike a standard Telegram invite link, this resource is a managed business asset.

It supports:

- Worker assignment
- Versioning
- Regeneration
- Restoration
- History
- Search
- Migration
- Audit

---

Philosophy

A Telegram channel belongs to the platform.

A Channel Link is assigned to a worker.

The worker never owns the channel.

The administrator always controls the assignment.

---

Responsibilities

The Channel Link Resource is responsible for:

- Creating invite links
- Assigning links to workers
- Maintaining link history
- Maintaining channel short codes
- Regenerating links
- Restoring previous links
- Recording version history
- Supporting search
- Supporting migration

It does not manage:

- Worker identity
- Instagram accounts
- Training files
- Timeline history

---

Ownership

Primary Owner:

Channel Link Module

Only this module may create, update, archive, or restore channel links.

---

Resource Lifetime

Property| Value
Created| During onboarding or regeneration
Updated| When regenerated or reassigned
Archived| When replaced
Deleted| Never (archive instead)

---

Channel Philosophy

Each worker always has one current active invite link.

Previous links remain available in history.

Example:

Worker WK-154

↓

Version 1

↓

Version 2

↓

Version 3 (Current)

---

Channel Short Code

Every active channel assignment receives a permanent short code.

Example:

GPA-WK154-V1

GPA-WK154-V2

GPA-WK6456-V1

Rules:

- Human readable
- Unique
- Searchable
- Never edited after creation

The Short Code is the administrative identity of the assignment.

---

Invite Link Name

Telegram invite links should use a compact naming convention.

Example:

GPA-WK154-V2

Additional metadata should be stored separately:

- Creation Date
- Reason
- Created By
- Version

This keeps the Telegram-side name short while preserving detailed history in the database.

---

Channel Assignment

Each worker has exactly one active Channel Link assignment.

Relationship:

Worker

↓

Channel Link

↓

Telegram Channel

The Worker Resource stores only the current reference.

---

Link Version

Every regenerated link creates a new version.

Example:

Version 1

↓

Version 2

↓

Version 3

Older versions remain archived.

Versions are immutable.

---

Link History

History stores:

- Version
- Invite Link
- Short Code
- Creation Date
- Replacement Date
- Reason
- Administrator
- Status

History is append-only.

---

Regeneration

Administrators may regenerate links when required.

Supported reasons:

- Security
- Campaign Update
- Worker Request
- Channel Maintenance
- Manual Replacement
- Other

Regeneration never changes the Worker ID.

---

Link Restoration

Administrators may restore any previous archived link.

When restored:

- The restored link becomes current.
- A new Timeline entry is created.
- Worker references are updated.

No new Worker ID or Channel Short Code is created during restoration of the same version.

---

Search Support

The Channel Link Resource must support searching by:

- Worker ID
- Channel Short Code
- Invite Link
- Version
- Telegram Channel ID

Every successful search should provide:

- Open Worker Profile
- Open Link History
- Copy Short Code
- Copy Invite Link

---

Current Scope

This part defines:

- Purpose
- Ownership
- Channel Assignment
- Short Codes
- Invite Link Naming
- Versioning
- History
- Search

The following parts will define:

- Regeneration Workflow
- Timeline Integration
- Audit Rules
- Migration
- Security
- Health Checks
- Recovery
- Implementation Notes
- Complete Resource Diagram

---

End of Part 1

14_Channel_Link_Resource.md (Part 2)

«Document Version: 1.0
Status: In Progress
Module: Channel Link Resource
Priority: Critical»

---

Link Generation Workflow

Every new Channel Link should follow the same workflow.

Administrator

↓

Select Worker

↓

Select Telegram Channel

↓

Generate Invite Link

↓

Generate Short Code

↓

Create Link Version

↓

Update Worker Resource

↓

Create Timeline Entry

↓

Notify Worker

The generation process must always be deterministic and auditable.

---

Link Generation Rules

Every generated link must satisfy:

- Unique active invite link
- Valid Telegram channel
- Existing Worker
- Existing Worker ID
- Generated Short Code
- Link Version
- Audit Record

The system should reject incomplete assignments.

---

Channel Assignment Rules

Each worker may have:

- One active channel assignment
- Multiple archived assignments

Each channel may contain:

- Multiple workers
- Multiple invite links

The worker never joins the channel automatically.

The assigned invite link is only used for Instagram profile placement.

---

Channel Short Code Rules

The Channel Short Code is the primary administrative identifier.

Example:

GPA-WK154-V2

Structure:

<Project Prefix>-<Worker ID>-<Version>

Examples:

GPA-WK154-V1

GPA-WK154-V2

GPA-WK6456-V1

GPA-WK12054-V4

The format must support future Worker IDs without redesign.

---

Link Version Rules

Version numbers always increase.

Example:

V1

↓

V2

↓

V3

↓

V4

Rules:

- Never decrease.
- Never reuse.
- Never edit previous versions.

---

Regeneration Workflow

Current Link

↓

Admin Request

↓

Generate New Invite Link

↓

Create New Version

↓

Archive Previous Version

↓

Update Worker Reference

↓

Timeline

↓

Worker Notification

The worker always receives the newest active link.

---

Restoration Workflow

Administrators may restore any archived version.

Workflow:

Archived Version

↓

Administrator

↓

Restore

↓

Validation

↓

Activate

↓

Worker Updated

↓

Timeline

↓

Notification

Restoration preserves historical records.

---

Link History

Every generated link should record:

- Link Version
- Invite Link
- Channel Short Code
- Worker ID
- Channel ID
- Generated By
- Generation Date
- Replacement Date
- Status
- Reason

History is append-only.

---

Reason Tracking

Every regeneration should include a reason.

Examples:

- Security
- Worker Request
- Campaign Update
- Channel Maintenance
- Mistake Correction
- Manual Replacement

Reasons improve auditing and troubleshooting.

---

Worker Experience

Workers should only see:

- Current active invite link

Workers should not see:

- Version numbers
- History
- Archived links
- Channel IDs
- Internal metadata

The interface should remain simple.

---

Administrator Experience

Administrators should see:

- Active Link
- Current Version
- Short Code
- Link History
- Restore Button
- Regenerate Button
- Copy Link
- Copy Short Code
- Open Worker Profile

Every administrative page displaying a Channel Link should also provide a direct way to open the related Worker Profile.

---

Copy Behaviour

To reduce mistakes:

Clicking the Short Code should copy only:

GPA-WK154-V2

Clicking the Invite Link should copy only the invite link.

Opening the Worker Profile should always be a separate action.

---

Timeline Integration

The following actions generate Timeline events:

- Link Created
- Link Regenerated
- Link Restored
- Link Assigned
- Link Removed

Timeline events should reference:

- Worker ID
- Link Version
- Short Code

---

Audit Integration

Administrative actions requiring audit:

- Generate Link
- Restore Link
- Manual Assignment
- Force Replacement
- Manual Archive

Audit records should include:

- Administrator
- Timestamp
- Worker ID
- Link Version
- Reason

---

Search Integration

Supported searches:

- Worker ID
- Channel Short Code
- Invite Link
- Version
- Telegram Channel ID

Search results should always provide:

- Worker Profile
- Link History
- Timeline

---

Remaining Sections

The final part will define:

- Migration
- Security
- Health Checks
- Performance Guidelines
- Recovery
- Resource Diagram
- Implementation Notes
- Final Specification

---

End of Part 2

14_Channel_Link_Resource.md (Part 3)

«Document Version: 1.0
Status: Approved
Module: Channel Link Resource
Priority: Critical»

---

Migration Support

The Channel Link Resource must fully support migration between bot versions.

Migration should preserve:

- Current Active Link
- Current Channel Short Code
- Link Version
- Link History
- Current Assignment
- Resource References

Workers should continue using the same active link after migration unless administrators decide otherwise.

---

Recovery Policy

If a channel link is accidentally replaced or archived:

Administrators may restore a previous version.

Recovery should restore:

- Invite Link
- Channel Short Code
- Version Reference
- Worker Reference

Recovery should never generate duplicate versions.

---

Health Check Rules

The Health Checker should verify:

- Worker reference exists.
- Telegram channel exists.
- Active invite link exists.
- Only one active link per worker.
- Channel Short Code uniqueness.
- Version sequence integrity.
- Link history integrity.

Errors should be reported to the Error Log Channel.

Automatic repair is optional and should require administrator approval.

---

Resource Integrity Rules

Every active Channel Link must satisfy:

✓ Existing Worker

✓ Existing Telegram Channel

✓ Existing Invite Link

✓ Existing Short Code

✓ Valid Version

✓ Active Status

Broken or orphaned records are not allowed.

---

Security Rules

Workers may:

- View the current invite link.
- Copy the invite link.

Workers may not:

- View archived links.
- View version history.
- Generate links.
- Restore links.
- View channel metadata.
- View administrative notes.

---

Administrator Permissions

Permission examples:

Action| Secondary Admin| Super Admin
View Link| ✅| ✅
Copy Link| ✅| ✅
Copy Short Code| ✅| ✅
Generate Link| Optional| ✅
Regenerate Link| Optional| ✅
Restore Link| Optional| ✅
View History| Optional| ✅
Delete History| ❌| ❌

Link history should never be manually deleted.

---

Performance Guidelines

The Channel Link Resource should never store:

- Worker Profile
- Telegram Messages
- Screenshots
- Media Files

Only store:

- References
- Metadata
- Version Information

This keeps the resource lightweight.

---

Search Optimization

The Channel Link Resource should support indexed search by:

- Worker ID
- Channel Short Code
- Invite Link
- Telegram Channel ID
- Link Version

Every result should allow quick navigation to the Worker Profile.

---

Resource Relationships

Worker Resource
        │
        ▼
Channel Link Resource
        │
        ├── Telegram Channel
        ├── Invite Link
        ├── Link History
        ├── Timeline
        └── Audit

The Worker Resource owns the relationship.

The Channel Link Resource owns the operational link data.

---

Field Classification

The resource contains three categories.

Identity

- Link ID
- Worker Reference
- Channel Reference

---

Current Configuration

- Active Invite Link
- Active Version
- Active Short Code
- Current Status

---

Metadata

- Created Date
- Last Updated
- Last Regenerated
- Last Restored
- Last Verified

Historical information belongs to Link History.

---

Archive Policy

Archived links remain available for:

- Audit
- Timeline
- Historical Preview
- Migration
- Investigation

Archived links are never assigned automatically.

---

Backup Policy

Backups should preserve:

- Current Active Link
- Link History
- Current Version
- Worker References

Telegram invite links should never be regenerated during backup restoration unless they are invalid.

---

Future Expansion

The architecture supports future additions.

Examples:

- Multiple Channel Assignments
- Campaign-specific Links
- Link Expiration Policies
- Automatic Rotation
- QR Code Generation
- Analytics per Link
- Click Tracking (if supported)

Future features should extend this resource without redesign.

---

Implementation Notes

Resource Type

Operational Resource

---

Primary Owner

Channel Link Module

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

Yes

Every regenerated invite link creates a new version.

---

Archive Supported

Yes

---

Recovery Supported

Yes

---

Cache Friendly

Yes

Only current active assignment should be cached.

---

Final Specification Summary

The Channel Link Resource manages every Telegram invite link assigned to workers.

It provides:

- Controlled assignment
- Version history
- Restoration
- Administrative search
- Auditability
- Migration compatibility

while ensuring that workers always interact with only the currently assigned invite link.

---

Final Statement

The Channel Link Resource is the official specification for Telegram invite link management within IWMS.

All channel assignment, regeneration, restoration, migration, and administrative workflows must comply with this specification.

Future enhancements should extend this architecture while preserving compatibility with existing Worker Resources and Link History.

---

End of 14_Channel_Link_Resource.md
