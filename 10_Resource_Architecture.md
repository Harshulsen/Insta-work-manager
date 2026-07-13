10_Resource_Architecture.md

«Document Version: 1.0
Status: Approved
Module: Resource Architecture
Priority: Critical»

---

Purpose

This document defines the complete resource architecture of the Instagram Workforce Management System (IWMS).

Resources are the foundation of the entire platform.

Every feature, workflow, automation, notification, timeline, history, and administrator action ultimately operates on one or more resources.

This document defines:

- Resource Categories
- Resource Ownership
- Resource Relationships
- Resource Lifetime
- Resource Dependencies
- Resource Rules
- Resource Versioning
- Resource Naming Standards

No implementation should begin before this architecture is finalized.

---

What is a Resource?

A Resource is a logical storage unit responsible for one specific type of information.

Examples:

- Worker
- Instagram Account
- Work
- Timeline
- Notification
- Training
- Support Ticket

A resource is not a Telegram message.

A resource is not a screen.

A resource represents structured business data.

---

Resource Design Principles

Every resource must follow these principles.

- One responsibility
- One owner
- Clear lifecycle
- Searchable
- Auditable (when required)
- Versioned (when required)
- Scalable
- Independent

---

Resource Categories

IWMS divides resources into five categories.

---

1. Master Resources

Permanent business entities.

Examples:

- Workers
- Global Settings
- Global Resources
- Admin Profiles

Characteristics:

- Long lifetime
- Rarely deleted
- Frequently referenced

---

2. Operational Resources

Resources used during daily operations.

Examples:

- Works
- Notifications
- Reviews
- Support Tickets
- Bug Reports
- Slots

Characteristics:

- Frequently created
- Frequently updated
- Medium lifetime

---

3. Archive Resources

Historical information.

Examples:

- Timeline
- Snapshots
- Link History
- Training History
- Reward History

Characteristics:

- Append Only
- Never modified
- Never reused

---

4. Temporary Resources

Short-lived data.

Examples:

- Pending Upload
- Pending Screenshot
- Session Cache
- Temporary Validation

Characteristics:

- Automatically cleaned
- Never treated as history

---

5. Developer Resources

Used only inside Developer Mode.

Examples:

- Fake Workers
- Simulated Work
- Test Reports
- Load Test Results

Must never mix with production resources.

---

Resource Hierarchy

System

│

├── Workers

│     ├── Instagram Accounts

│     ├── Slots

│     ├── Training

│     ├── Works

│     ├── Notifications

│     ├── Timeline

│     ├── History

│     ├── Support

│     └── Bug Reports

│

├── Global Resources

├── Settings

├── Analytics

└── Developer

---

Resource Ownership

Every resource has exactly one owner.

Resource| Owner
Worker| Worker Module
Instagram Account| Instagram Module
Training| Training Module
Work| Work Module
Timeline| Timeline Module
Notification| Notification Module
Support Ticket| Support Module
Bug Report| Bug Report Module
Workspace| Workspace Module
Permission| Permission Module
Global Settings| System Module
Developer Data| Developer Module

No resource should have multiple owners.

---

Core Resources

The first release of IWMS includes the following core resources.

Workers

Instagram Accounts

Training

Works

Slots

Weekly Rewards

Notifications

Timeline

History

Support

Bug Reports

Search Index

Settings

Workspace

Permissions

Analytics

Developer

Every future feature should extend existing resources whenever possible.

---

Resource Relationships

Worker

│

├── Instagram Accounts

├── Slots

├── Training

├── Works

├── Timeline

├── Notifications

├── Support Tickets

├── Bug Reports

├── Weekly Rewards

└── History

Worker is the central business entity.

---

Relationship Rules

Relationships should follow these principles.

- Parent before Child
- One Direction
- No Circular References
- No Duplicate Ownership

---

Resource Lifetime

Resource| Lifetime
Worker| Permanent
Instagram Account| Replaceable
Work| Archive After Completion
Notification| Temporary
Timeline| Permanent
History| Permanent
Settings| Permanent
Developer Data| Temporary

---

Resource States

Every resource maintains its own state.

Example:

Worker

↓

Active

Instagram

↓

Ready

Work

↓

Submitted

Timeline

↓

Append Only

Notifications

↓

Delivered

State Management controls behavior.

---

Resource Versioning

Versioning applies only when history must be preserved.

Current versioned resources:

- Training
- Profile Photos
- Invite Links
- Setup Configuration

Future resources may also become versioned.

---

Resource Snapshots

Snapshots preserve previous resource state before major changes.

Example:

Training

↓

Snapshot

↓

Update

↓

New Version

Snapshots are immutable.

---

Resource Identifiers

Every resource receives a unique identifier.

Examples:

WK-154

IG-458

WRK-7851

TRN-102

TL-9854

NOT-4521

SUP-782

BUG-914

APR-215

Identifiers are permanent.

---

Resource Searchability

Every major resource should be searchable.

Supported search keys include:

- Worker ID
- Telegram ID
- Username
- Name
- Instagram Username
- Channel Short Code
- Work ID
- Support ID
- Bug ID

Search must always return the correct object.

---

Resource Validation

Every write operation follows this order.

Input

↓

Validation

↓

Ownership Check

↓

Permission Check

↓

State Check

↓

Database

↓

Timeline

↓

Notification

---

Resource Isolation

Resources should never directly manipulate unrelated resources.

Example:

Training Resource

❌ Should not modify Rewards.

Reward Module

❌ Should not modify Instagram Accounts.

Communication must occur through business logic.

---

Resource Audit

The following resources require audit support.

- Worker
- Permissions
- Weekly Rewards
- Settings
- Migration
- Worker Removal

Audit records must include:

- Who
- What
- When
- Why

---

Resource Security

Resources should expose only the minimum required information.

Worker Interface

↓

Worker Data Only

Admin Interface

↓

Permission Controlled

Developer Mode

↓

Testing Resources Only

---

Resource Scalability

Every resource should support future expansion without redesign.

Examples:

Workers

↓

Multiple Campaigns

Works

↓

Multiple Task Types

Training

↓

Multiple Programs

Notifications

↓

Multiple Delivery Methods

---

Resource Recovery

Critical resources should support recovery whenever possible.

Examples:

- Worker
- Training
- Invite Link
- Settings

Developer resources are excluded.

---

Resource Deletion Policy

Deletion rules differ by resource type.

Resource| Policy
Worker| Soft Remove → Permanent Delete
Timeline| Never Delete
History| Never Delete
Notifications| Auto Cleanup
Temporary Data| Auto Cleanup
Developer Data| Auto Cleanup

---

Future Expansion

Potential future resources:

- Referral Resource
- Campaign Resource
- AI Review Resource
- Finance Resource
- Web Session Resource
- API Resource

New resources must follow this architecture before implementation.

---

Final Statement

Resource Architecture is the foundation of the IWMS database.

Every future resource must:

- Have one owner.
- Have one responsibility.
- Define its lifecycle.
- Define its relationships.
- Define its state.
- Define its identifier.
- Define its versioning policy.
- Define its deletion policy.

No undocumented resource should exist within the system.

---

End of Document
