09_Data_Flow_Architecture.md

«Document Version: 1.0
Status: Approved
Module: Data Flow Architecture
Priority: Critical»

---

Purpose

This document defines how information moves throughout the Instagram Workforce Management System (IWMS).

Rather than describing features, this document explains the journey of data from the moment it enters the system until it is processed, stored, logged, and presented to users.

Every module, automation engine, database resource, notification, and administrative action must follow these data flow principles.

---

Philosophy

Data should never move randomly.

Every piece of data must follow a predictable and auditable path.

Every request must pass through the same architectural layers.

No module should bypass validation or business rules.

---

Core Data Flow

Every operation follows the same pipeline.

Input

↓

Validation

↓

Business Rules

↓

Permission Check

↓

State Check

↓

Database Update

↓

Automation

↓

Timeline

↓

Notifications

↓

Response

This pipeline applies to both workers and administrators.

---

Data Flow Layers

The system is divided into logical processing layers.

Telegram

↓

Interface Layer

↓

Validation Layer

↓

Business Logic Layer

↓

Permission Layer

↓

State Management Layer

↓

Database Layer

↓

Automation Layer

↓

Timeline Layer

↓

Notification Layer

↓

Response Layer

Each layer has one responsibility.

---

Layer Responsibilities

Interface Layer

Receives user interaction.

Examples:

- Button Click
- Message
- Screenshot
- Command

No business decisions occur here.

---

Validation Layer

Verifies received information.

Examples:

- Instagram Link Format
- Screenshot Presence
- Slot Availability
- Language Selection

Invalid data never proceeds.

---

Business Logic Layer

Applies project rules.

Examples:

- Worker eligible?
- Training completed?
- Slot active?
- Work allowed?
- Account update required?

---

Permission Layer

Checks administrative permissions.

Examples:

- Can approve work?
- Can delete worker?
- Can restore backup?
- Can assign bonus?

Workers bypass this layer because they have no administrative permissions.

---

State Management Layer

Confirms current object state.

Examples:

Worker

↓

Active?

↓

Continue

Worker

↓

Removed?

↓

Reject Request

No operation ignores state.

---

Database Layer

Stores current state.

Responsibilities:

- Create
- Update
- Archive
- Version
- Snapshot

Database never decides business rules.

---

Automation Layer

Runs background actions.

Examples:

- Schedule Work
- Weekly Reset
- Cleanup
- Reminder
- Migration

Automation reacts to state changes.

---

Timeline Layer

Creates historical events.

Every important operation generates a timeline entry.

---

Notification Layer

Determines who should receive information.

Possible targets:

- Worker
- Admin
- Workspace

---

Response Layer

Returns final response.

Examples:

- Success
- Error
- Next Step
- Updated Dashboard

---

Worker Data Flow

Example:

Worker submits Instagram account.

Worker

↓

Telegram Bot

↓

Validate Instagram Link

↓

Business Rules

↓

Worker State

↓

Instagram Resource

↓

Worker Timeline

↓

Notification

↓

Next Step

---

Training Flow

Training Assigned

↓

Training Resource

↓

Worker Resource

↓

Training Version

↓

Training Snapshot

↓

Training Center

↓

Worker

Snapshots are created before significant changes.

---

Work Assignment Flow

Scheduler

↓

Slot Engine

↓

Worker Eligibility

↓

Generate Work Package

↓

Store Work

↓

Send Notification

↓

Worker

Work is never sent without eligibility verification.

---

Screenshot Submission Flow

Worker

↓

Upload Screenshot

↓

Validate

↓

Store Submission

↓

Review Queue

↓

Timeline

↓

Admin Notification

Submission does not imply approval.

---

Review Flow

Admin

↓

Permission Check

↓

Review

↓

Decision

↓

Update Work

↓

Timeline

↓

Worker Notification

---

Weekly Reward Flow

Approved Work

↓

Weekly Review

↓

Bonus

↓

Final Approval

↓

Reward Record

↓

Worker Notification

Rewards remain locked until approval.

---

Support Flow

Worker

↓

Support Ticket

↓

Support Workspace

↓

Admin Reply

↓

Worker

Communication always passes through the Support Module.

---

Bug Report Flow

Worker

↓

Bug Report

↓

Bug Workspace

↓

Investigation

↓

Resolution

↓

Worker

---

Instagram Replacement Flow

Worker Request

↓

Validation

↓

Admin Review

↓

Replace Account

↓

Update Worker

↓

Timeline

↓

Continue Working

Worker identity remains unchanged.

---

Channel Link Flow

Administrator

↓

Generate Link

↓

Assign Worker

↓

Create Version

↓

Update Worker

↓

Timeline

↓

Training Center

Old versions remain archived.

---

Slot Flow

Worker

↓

Select Slots

↓

Validation

↓

Availability Check

↓

Store Schedule

↓

Scheduler

Future work depends on stored slots.

---

Notification Flow

Every notification follows the same process.

Event

↓

Notification Engine

↓

Target Selection

↓

Queue

↓

Delivery

↓

Log

Notifications are never sent directly.

---

Timeline Flow

Successful Operation

↓

Generate Timeline Event

↓

Store

↓

Reference Related Objects

Timeline remains chronological.

---

Snapshot Flow

Current Configuration

↓

Change Requested

↓

Create Snapshot

↓

Apply Change

↓

Store Version

History is never overwritten.

---

Migration Flow

Old Bot

↓

Export Resources

↓

Migration Package

↓

Import

↓

Validation

↓

Restore

↓

Worker Continues

Migration preserves progress.

---

Admin Action Flow

Admin

↓

Permission Check

↓

Business Rules

↓

Database

↓

Timeline

↓

Notification

↓

Response

Dangerous actions may require approval.

---

Approval Flow

Secondary Admin

↓

Approval Request

↓

Approval Center

↓

Super Admin

↓

Approve

↓

Execute Action

↓

Timeline

↓

Notification

Rejected requests terminate immediately.

---

Search Flow

Search Input

↓

Identifier Detection

↓

Search Engine

↓

Object Resolution

↓

Open Worker Profile

Every identifier resolves consistently.

---

Logging Flow

System Event

↓

Log Engine

↓

Normal Log

OR

Error Log

Logs remain separate from operational workflows.

---

Developer Mode Flow

Developer Action

↓

Simulation

↓

Temporary Database

↓

Results

↓

Reports

Production data remains isolated.

---

Error Flow

Whenever an operation fails:

Failure

↓

Rollback (if applicable)

↓

Error Log

↓

Timeline

↓

User-Friendly Response

Internal errors should never expose technical details to workers.

---

Data Ownership Rule

Every piece of information belongs to one owner.

Possible owners:

- Worker
- Instagram Account
- Work
- Training
- Notification
- Support Ticket
- Bug Report
- System

Ownership determines update authority.

---

Data Integrity Rules

Every data operation must satisfy:

- Validation
- State Check
- Permission Check
- Resource Ownership
- Timeline Generation
- Audit (if required)

---

Performance Principles

The architecture should minimize unnecessary processing.

Examples:

- Load only required resources.
- Avoid duplicate writes.
- Reuse cached global resources where appropriate.
- Archive historical data separately from current state.

---

Future Expansion

Future modules must integrate into the same flow architecture.

Examples:

- AI Review
- Referral System
- Web Dashboard
- Multiple Campaigns

New modules must not bypass the defined processing pipeline.

---

Final Statement

The Data Flow Architecture defines how information moves throughout IWMS.

Every module, automation engine, database resource, developer tool, and administrator action must follow these processing layers and flow rules.

This document ensures predictable behavior, consistent validation, strong auditability, and long-term maintainability.

---

End of Document
