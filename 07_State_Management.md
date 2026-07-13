07_State_Management.md

«Document Version: 1.0
Status: Approved
Module: State Management
Priority: Critical»

---

Purpose

This document defines the official state management architecture used throughout the Instagram Workforce Management System (IWMS).

Every worker, work assignment, Instagram account, support ticket, review, notification, and administrative process operates using predefined states.

State management ensures predictable automation, easier debugging, and consistent system behavior.

---

Philosophy

Every object inside the system should always exist in one clearly defined state.

A state represents the current condition of an object.

Objects never exist in undefined or partially known conditions.

---

Why State Management Exists

The platform contains multiple independent modules.

Examples:

- Worker
- Instagram Account
- Work
- Review
- Training
- Support
- Bug Report
- Migration

Without standardized states, each module would behave differently.

State Management provides one common language for the entire platform.

---

State Rules

Every state must satisfy these rules.

- Every state has one meaning.
- States are mutually exclusive unless explicitly documented.
- State transitions follow predefined rules.
- Invalid transitions are rejected.
- Every important state change generates a Timeline event.
- Every high-risk state transition creates an Audit Record.

---

Worker State Machine

A worker always belongs to one primary state.

---

New

Worker has started the bot but has not yet applied.

Allowed transitions:

→ Applying

---

Applying

Worker is completing onboarding.

Includes:

- Language selection
- Instagram submission

Allowed transitions:

→ Training

---

Training

Worker is completing setup.

Allowed transitions:

→ Verification Pending

---

Verification Pending

Worker has submitted setup screenshots.

Waiting for verification.

Allowed transitions:

→ Active

→ Training (if setup must be repeated)

---

Active

Worker is fully operational.

Can:

- Receive work
- View dashboard
- Open training
- Contact support

Allowed transitions:

→ Vacation

→ Needs Update

→ Suspended

→ Removed

---

Needs Update

Worker must update one or more required resources.

Examples:

- Instagram Account
- Bio
- Invite Link
- Profile Photo

The worker receives notifications instead of work until the required updates are completed.

Allowed transitions:

→ Active

---

Vacation

Temporary pause requested by the worker.

Allowed transitions:

→ Active

---

Suspended

Temporary administrative restriction.

Worker cannot receive work.

Allowed transitions:

→ Active

→ Removed

---

Appeal Pending

Worker has submitted an appeal after removal.

Allowed transitions:

→ Active

→ Removed

---

Removed

Worker is removed from active workforce.

Depending on system configuration:

- Appeal Allowed
- Appeal Disabled

Allowed transitions:

→ Appeal Pending

→ Deleted

---

Deleted

Final irreversible state.

Worker resources are removed according to retention policy.

Only audit records remain.

No further transitions are allowed.

---

Worker State Diagram

New

↓

Applying

↓

Training

↓

Verification Pending

↓

Active

↓

Vacation

↓

Active

↓

Needs Update

↓

Active

↓

Suspended

↓

Active

↓

Removed

↓

Appeal Pending

↓

Active

OR

Deleted

---

Instagram Account States

Every Instagram account maintains its own independent state.

---

Registered

Account has been submitted.

---

Pending Setup

Worker has not completed setup.

---

Ready

Account is fully configured.

---

Needs Update

Administrator requires modifications.

---

Replacement Requested

Worker requested replacement.

---

Replaced

Account is archived.

New account becomes active.

---

Disabled

Account cannot currently be used.

---

Work States

Each work assignment maintains its own lifecycle.

---

Scheduled

Work created.

Waiting for slot.

---

Sent

Delivered to worker.

---

In Progress

Worker is expected to complete work.

---

Submission Pending

Waiting for screenshots.

---

Submitted

Screenshots received.

---

Under Review

Administrator review in progress.

---

Approved

Accepted.

Eligible for weekly reward.

---

Rejected

Rejected.

History preserved.

---

Missed

Deadline expired.

---

Cancelled

Cancelled before completion.

---

Work State Diagram

Scheduled

↓

Sent

↓

In Progress

↓

Submitted

↓

Under Review

↓

Approved

OR

Rejected

OR

Missed

---

Training States

Training follows its own lifecycle.

---

Not Started

---

In Progress

---

Completed

---

Requires Update

---

Reassigned

---

Support Ticket States

Support tickets operate independently.

---

Open

---

Assigned

---

Waiting for Worker

---

Waiting for Admin

---

Resolved

---

Closed

---

Bug Report States

---

Reported

---

Verified

---

In Investigation

---

Fixed

---

Closed

---

Review States

Screenshot reviews follow their own workflow.

---

Pending

---

Reviewing

---

Approved

---

Rejected

---

Needs Manual Review

Reserved for future expansion.

---

Weekly Reward States

---

Locked

Worker cannot view reward.

---

Under Review

Administrative evaluation.

---

Approved

Reward finalized.

---

Paid

Reward completed.

---

Migration States

---

Ready

---

Exported

---

Imported

---

Verified

---

Completed

---

Failed

---

Notification States

---

Scheduled

---

Sent

---

Delivered

---

Read

---

Expired

---

Channel Link States

---

Active

Current assigned link.

---

Archived

Historical link.

---

Reused

Old link reassigned.

---

Invalid

No longer usable.

---

Workspace States

Each workspace maintains its own connection state.

---

Connected

---

Permission Error

---

Disabled

---

Missing

---

Developer States

Developer environment has separate states.

---

Safe Mode

Testing isolated.

---

Simulation Running

---

Stress Testing

---

Maintenance

---

State Transition Rules

Every transition must satisfy:

- Validation
- Business Rules
- Permission Check
- Timeline Entry
- Notification (if required)
- Audit Record (if required)

No transition may bypass validation.

---

Invalid State Transitions

Examples:

Deleted

↓

Active

❌ Not Allowed

---

Approved Work

↓

Scheduled

❌ Not Allowed

---

Removed Worker

↓

Training

❌ Not Allowed

---

State Ownership

Each module owns its own states.

Module| Owns States
Worker| Worker States
Instagram| Account States
Work| Work States
Training| Training States
Review| Review States
Support| Ticket States
Bug Reports| Bug States
Migration| Migration States

---

Timeline Integration

Every significant state transition generates a Timeline event.

Example:

Worker

↓

Vacation

↓

Timeline Entry

↓

Notification

---

Automation Integration

Automation reacts only to state changes.

Example:

Worker

↓

Needs Update

↓

Automation

↓

Stop Work Assignment

↓

Notify Worker

---

Future Expansion

Additional states may be introduced for:

- AI Review
- Multiple Campaigns
- Multiple Businesses
- Quality Scoring

New states must be documented before implementation.

---

Final Statement

State Management is the behavioral foundation of IWMS.

Every module, automation engine, workflow, notification, database resource, and administrator interface must operate according to the state definitions contained in this document.

No undocumented state may be introduced into the system.

---

End of Document
