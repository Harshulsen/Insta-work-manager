03_Design_Principles.md

«Document Version: 1.0
Status: Approved
Module: Core Architecture
Priority: Critical»

---

Purpose

This document defines the architectural principles that every future design, feature, module, automation, database structure, and implementation must follow.

These principles are considered project rules, not suggestions.

No future AI, developer, or contributor should violate these principles without documenting and approving the change.

---

Philosophy

The system is designed around one simple idea:

«Workers should experience simplicity. Administrators should experience power. Developers should experience structure.»

Every decision made throughout the project must support this philosophy.

---

Principle 1 — Simplicity First

The worker interface must remain as simple as possible.

Workers should never be exposed to internal architecture.

Examples of hidden complexity:

- Resource IDs
- Version numbers
- Timeline records
- Internal mappings
- Database structure
- Channel history
- Snapshot history
- Automation rules

Workers only receive information required to complete their current task.

---

Principle 2 — Backend Complexity is Acceptable

The backend may become complex if it improves:

- reliability
- scalability
- maintainability
- auditing
- debugging

Complexity belongs to the system, not to the worker.

---

Principle 3 — Modular Architecture

Every major feature must exist as an independent module.

Examples:

- Worker System
- Training System
- Slot System
- Review System
- Notification Engine
- Automation Engine
- Workspace System
- Permission System

Modules should communicate through defined resources rather than direct dependencies whenever possible.

---

Principle 4 — Single Responsibility

Each module must have one primary responsibility.

Examples:

Workers Resource

Responsible only for worker identity and current references.

Instagram Resource

Responsible only for Instagram accounts.

Training Resource

Responsible only for training data.

Timeline

Responsible only for historical events.

No module should become responsible for unrelated functionality.

---

Principle 5 — Separation Between Worker and Account

Workers are permanent.

Instagram accounts are temporary.

A worker may replace Instagram accounts multiple times.

The system should therefore manage:

Worker

↓

Instagram Accounts

rather than treating Instagram accounts as permanent identities.

---

Principle 6 — Version Instead of Overwrite

Whenever information may be required in the future for auditing or restoration, the system should create a new version instead of overwriting the previous one.

Examples:

- Training Versions
- Channel Link Versions
- Profile Photo Versions
- Setup Versions
- Snapshot Versions

---

Principle 7 — Snapshot Before Change

Before any major change affecting worker resources, the system should preserve a snapshot whenever practical.

Examples:

Training Update

↓

Training Snapshot

Channel Update

↓

Channel Snapshot

Work Assignment

↓

Work Snapshot

Snapshots preserve historical state.

---

Principle 8 — Timeline for Every Important Event

Every important operation should generate a timeline event.

Examples:

Worker Joined

Training Completed

Channel Changed

Instagram Changed

Weekly Reward Approved

Worker Removed

Timeline exists for auditing and debugging.

---

Principle 9 — Admin Has Full Control

Administrators must remain capable of overriding automation whenever required.

Examples:

- Force training
- Force account replacement
- Change channel link
- Pause work
- Resume work
- Assign bonus
- Replace profile photos
- Restore previous setup

Automation should assist administrators, not replace them.

---

Principle 10 — Worker Never Loses Progress

Unless intentionally deleted by a Super Admin, workers should continue from where they previously stopped.

Examples:

Bot migration

↓

Worker resumes.

System update

↓

Worker resumes.

Maintenance

↓

Worker resumes.

---

Principle 11 — Migration Support

The architecture must support future migration.

Migration should preserve:

- Worker Identity
- Training
- Instagram Accounts
- History
- Rewards
- Timeline
- Current Progress

Migration must not require workers to register again.

---

Principle 12 — Everything Important is Searchable

Administrators should never manually browse large datasets.

The system should support searching by:

- Worker ID
- Telegram ID
- Username
- Name
- Instagram Username
- Channel Link
- Channel Short Code
- Invite Link
- Work ID
- Ticket ID

Search should reach the worker profile from every supported identifier.

---

Principle 13 — Context Preservation

Whenever administrators open a worker profile from another module, the system should remember the previous page.

Returning should restore the original context.

Examples:

Review Queue

↓

Worker Profile

↓

Back

↓

Review Queue

The administrator should never lose workflow position.

---

Principle 14 — Permission Before Visibility

Permissions should determine interface visibility.

If a user lacks permission:

The button should not appear.

Hidden functionality is safer than disabled functionality.

---

Principle 15 — Permission Based Administration

Administration is permission-based.

Not role-based.

Each administrator receives only the permissions required.

Temporary permissions must also be supported.

---

Principle 16 — High-Risk Actions Require Approval

Dangerous operations should support approval workflows.

Examples:

- Worker deletion
- Worker removal
- Database restore
- Migration
- Major settings changes
- Large bonus approval

Approval requests should be sent to the dedicated Approval Center.

---

Principle 17 — Dedicated Workspaces

Operational activities should be separated into dedicated Telegram groups/channels.

Examples:

- Screenshot Review
- Support
- Bug Reports
- Logs
- Error Logs
- Weekly Reviews
- Approval Center

The administrator's private bot chat should remain clean.

---

Principle 18 — Logs Never Mix With Operations

Operational messages and system logs should remain separated.

Workers should never generate unnecessary clutter in admin conversations.

---

Principle 19 — Resource Ownership

Every piece of data must have exactly one owner.

Possible owners:

- Worker
- Instagram Account
- Work
- Training
- Global Resource
- System

Ownership prevents duplication.

---

Principle 20 — Current State and History Must Be Separate

The system should distinguish between:

Current State

and

Historical Records.

Current resources remain lightweight.

Historical resources preserve evidence.

---

Principle 21 — Automation Must Be Predictable

Automation should always follow documented rules.

No hidden behaviour.

No random decision making unless explicitly configured.

---

Principle 22 — Testing Before Production

Every major feature should be tested before production deployment.

Developer tools should support:

- Fake Workers
- Fake Works
- Time Simulation
- Load Testing
- Scenario Testing
- Health Checks

Testing should not affect production workers.

---

Principle 23 — Production and Testing Must Remain Isolated

Developer Mode must never modify production data unless explicitly approved.

Testing environments should remain independent.

---

Principle 24 — Human Review Before Payment

Work completion does not automatically generate payment.

Flow:

Worker submits work

↓

Admin reviews

↓

Admin approves

↓

Weekly reward becomes eligible

Human review always has final authority.

---

Principle 25 — Hidden Earnings

Workers should not see estimated earnings during the week.

Instead, workers should see:

Weekly Reward

Locked 🔒

Available after weekly review.

The final reward is determined after review.

---

Principle 26 — Dynamic Configuration

Business rules should be configurable whenever possible.

Examples:

- Required Instagram Accounts
- Reels Per Work
- Daily Slots
- Training Resources
- Bonus Rules
- Weekly Limits

Avoid hardcoded values.

---

Principle 27 — Recovery Over Restart

Whenever possible, the system should recover rather than restart.

Examples:

Worker changes account

↓

Update setup

↓

Continue working

Instead of forcing complete registration again.

---

Principle 28 — Every Major Action Should Be Auditable

The system should always be capable of answering:

Who performed the action?

When?

Why?

What changed?

Auditability is mandatory.

---

Principle 29 — Long-Term Scalability

The architecture should support future expansion without redesign.

Examples:

- AI Review
- Web Dashboard
- Additional Task Types
- Multiple Campaigns
- Multiple Businesses

Scalability is preferred over short-term convenience.

---

Principle 30 — Future Ideas Do Not Interrupt Current Planning

Ideas discovered during development should not immediately change architecture.

Instead:

Record

↓

Review

↓

Implement later if approved.

This prevents endless planning loops.

---

Principle 31 — Worker Experience Is Sacred

This is the highest priority principle.

Whenever two solutions exist:

Choose the solution that is easier for the worker.

Even if backend implementation becomes more complex.

---

Architecture Decision Rule

Before adding any future feature, answer these questions:

1. Who owns the data?
2. Which resource stores it?
3. Is versioning required?
4. Is history required?
5. Is migration required?
6. Who can access it?
7. Does it affect worker simplicity?
8. Does it follow modular architecture?

Only after answering these questions should implementation begin.

---

Final Statement

This document defines the architectural foundation of the entire project.

Every future planning document, database resource, automation rule, admin panel, developer tool, and implementation must follow these principles.

If a future design conflicts with these principles, the conflict must be documented, reviewed, and approved before implementation.

---

End of Document
