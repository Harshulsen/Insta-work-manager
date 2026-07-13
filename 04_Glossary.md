04_Glossary.md

«Document Version: 1.0
Status: Approved
Module: Project Terminology
Priority: Critical»

---

Purpose

This document defines the official terminology used throughout the Instagram Workforce Management System (IWMS).

Every planning document, database resource, workflow, automation engine, developer tool, and implementation must use the definitions provided here.

This document serves as the single source of truth for project terminology.

---

Rules

- Every important term must have one official meaning.
- A term must never represent multiple concepts.
- Future documents must reference these definitions.
- New terminology should be added here before being used elsewhere.

---

General Terms

Worker

A Telegram user who has successfully joined the platform and performs assigned Instagram work.

A Worker is the primary user of the system.

---

Worker ID

A permanent unique identifier assigned to every worker.

Example:

WK-154

The Worker ID never changes during the worker's lifetime.

---

Telegram ID

The unique Telegram identifier provided by Telegram.

Used internally for authentication and migration.

Never shown as the primary identity.

---

Worker Profile

The complete permanent profile of a worker.

Contains:

- Identity
- Status
- Statistics
- References
- Current Configuration

---

Username

Telegram username of the worker.

Used only for searching and identification.

---

Language

Worker's preferred interface language.

Example:

- English
- Hinglish

---

Worker Status

Represents the worker's overall condition.

Examples:

- Pending Setup
- Active
- Vacation
- Suspended
- Removed
- Deleted

---

Worker Level

Represents worker performance.

Examples:

- Bronze
- Silver
- Gold
- Platinum

Worker Level is independent from weekly payment.

---

Season

One business week.

Every week starts a new Season.

A Season contains:

- Assigned Work
- Reviews
- Rewards
- Progress

---

Weekly Reward

The reward approved after administrative review.

Workers cannot view the reward before approval.

---

Bonus

An additional manual reward assigned by administrators.

Bonuses are optional.

---

Instagram Terms

Instagram Account

An Instagram account used by the worker to complete tasks.

Instagram Accounts are replaceable.

Workers are permanent.

Instagram Accounts are temporary.

---

Account Slot

Represents one required Instagram account.

Examples:

Account A

Account B

Account C

The number of Account Slots is configurable.

---

Replacement Count

The number of times an Instagram account has been replaced.

Stored separately for history and analytics.

---

Account Status

Current state of an Instagram account.

Examples:

- Active
- Needs Update
- Disabled
- Replaced

---

Training Terms

Training

The onboarding process required before a worker receives work.

---

Training Center

A permanent section where workers can reopen their assigned training resources.

---

Global Resource

A resource shared by every worker.

Examples:

- Setup Video
- Upload Tutorial
- Audio
- Bio Text

---

Worker Resource

A resource assigned individually to one worker.

Examples:

- Profile Photos
- Telegram Link
- Instagram Accounts

---

Training Version

A version number representing the current assigned training configuration.

---

Training Snapshot

A permanent historical record preserving a worker's complete training configuration at a specific point in time.

Snapshots are never overwritten.

---

Work Terms

Work

One assignment delivered to a worker.

Contains:

- Reels
- Caption
- Deadline

---

Work Package

The complete collection of reels assigned for one work session.

---

Slot

A scheduled working time selected by the worker.

Example:

09:00

13:00

20:00

---

Extra Work

A manually requested work assignment outside the worker's regular schedule.

---

Missed Work

A work assignment whose deadline expired before screenshot submission.

---

Work Snapshot

An immutable record preserving the original work assignment.

---

Verification Terms

Screenshot Submission

The process of submitting screenshots after completing assigned work.

The number of required screenshots equals the number of configured Instagram accounts.

---

Review Queue

A queue containing submitted work waiting for administrator review.

---

Approved Work

A reviewed work accepted by administrators.

---

Rejected Work

A reviewed work rejected by administrators.

---

Channel Terms

Telegram Invite Link

The unique Telegram invite link assigned to a worker.

Used inside Instagram.

---

Channel Short Code

A permanent identifier representing the assigned Telegram invite link.

Example:

GPA-WK154-V2

Used for searching and administration.

---

Link Version

Represents one generation of an assigned Telegram invite link.

---

Link History

Complete history of every link assigned to a worker.

---

Navigation Terms

Breadcrumb

A navigation mechanism allowing administrators to return to the previous page while preserving context.

---

Context

The previous screen or workflow from which the current page was opened.

---

Search System

The centralized system allowing administrators to locate workers using different identifiers.

---

Timeline Terms

Timeline

A chronological record of important worker events.

Examples:

- Joined
- Training Completed
- Link Changed
- Instagram Changed
- Reward Approved

---

Snapshot

A permanent copy of important system data captured before major changes.

---

Version

A numbered state representing one revision of a configurable resource.

---

Workspace Terms

Workspace

A Telegram group or channel dedicated to one operational purpose.

---

Screenshot Review Group

Workspace used to review submitted screenshots.

---

Support Group

Workspace where administrators manage support conversations.

---

Bug Report Group

Workspace used for technical issue reports.

---

Log Channel

Channel receiving operational logs.

---

Error Log Channel

Channel receiving system errors.

---

Approval Center

Private workspace used by the Super Admin to approve high-risk actions.

---

Permission Terms

Super Admin

Highest authority.

Has unrestricted access.

---

Secondary Admin

Administrator with limited permissions.

---

Permission

A single capability assigned to an administrator.

---

Temporary Permission

A permission automatically removed after a configured period.

---

Dual Confirmation

A workflow requiring Super Admin approval before completing high-risk actions.

---

Developer Terms

Developer Mode

Special environment used for testing.

Never affects production workers.

---

Fake Worker

Artificial worker generated for testing.

---

Health Check

Automatic validation of system consistency.

Detects:

- Missing Resources
- Invalid References
- Broken Configurations

---

Safe Mode

Testing mode isolated from production data.

---

Time Simulator

Developer tool used to simulate future time.

Example:

- One Hour
- One Day
- One Week

---

Stress Test

A simulated high-load environment used to validate scalability.

---

Migration Terms

Migration

Moving worker data from one bot version to another without restarting worker progress.

---

Migration Package

Structured data exported for migration.

Contains:

- Worker Identity
- Accounts
- Training
- Timeline
- Rewards
- Current Progress

---

System Terms

Resource

A logical storage unit responsible for one type of information.

Examples:

Workers

Instagram Accounts

Works

Timeline

Settings

---

Resource Owner

The primary entity responsible for a resource.

Examples:

- Worker
- Work
- Instagram Account
- Training
- Global System

---

Audit Record

A minimal permanent record preserved after irreversible actions.

Example:

Worker Deleted

Deleted By

Date

Reason

---

Future Terms

Additional terminology introduced in future versions of the project must be added to this document before use.

---

Final Statement

This glossary defines the official vocabulary of the Instagram Workforce Management System.

Every future planning document, implementation, automation engine, database resource, administrator interface, and developer tool must use these definitions consistently.

If a term is modified, the change must be documented and reflected across all related documents.

---

End of Document
