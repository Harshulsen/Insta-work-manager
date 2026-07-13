06_Worker_Lifecycle.md

«Document Version: 1.0
Status: Approved
Module: Worker Lifecycle
Priority: Critical»

---

Purpose

This document defines the complete lifecycle of a worker inside the Instagram Workforce Management System (IWMS).

It explains every state a worker can enter, every transition between those states, and the business rules governing each stage.

This document is considered the official reference for all worker-related workflows.

---

Philosophy

Every worker should experience one continuous journey.

The worker should never feel that different systems exist internally.

Regardless of how complex the backend becomes, the worker experience must always remain simple, consistent, and predictable.

---

High-Level Lifecycle

Discover Bot
        │
        ▼
Start Bot
        │
        ▼
Apply for Work
        │
        ▼
Language Selection
        │
        ▼
Instagram Account Registration
        │
        ▼
Training & Account Setup
        │
        ▼
Setup Verification
        │
        ▼
Worker Dashboard
        │
        ▼
Receive Work
        │
        ▼
Submit Screenshots
        │
        ▼
Review Queue
        │
        ▼
Weekly Review
        │
        ▼
Weekly Reward
        │
        ▼
Continue Working

This cycle repeats throughout the worker's lifetime.

---

Stage 1 — Discovery

The worker discovers the platform.

Possible sources:

- Referral
- Telegram Channel
- Friend
- Advertisement
- Existing Worker
- Future Marketing Campaigns

No worker data exists at this stage.

---

Stage 2 — Bot Start

The worker starts the Telegram bot.

The system verifies:

- Telegram ID
- Existing Worker
- Migrated Worker
- Removed Worker
- Blocked Worker

Possible outcomes:

- New Registration
- Continue Existing Profile
- Migration
- Appeal Screen
- Access Restricted

---

Stage 3 — Application

The worker chooses:

«Apply for Work»

The system introduces:

- Nature of work
- Basic expectations
- General requirements

The worker may continue or leave.

---

Stage 4 — Language Selection

The worker selects:

- English
- Hinglish

The selected language becomes the default interface language.

Language can be changed later from Settings.

---

Stage 5 — Instagram Account Registration

The worker submits Instagram account links.

Rules:

- Only valid Instagram links are accepted.
- Invalid links are rejected.
- Accounts are submitted one by one.
- Required account count is defined by the administrator.

Example:

Account 1

↓

Validation

↓

Accepted

↓

Account 2

↓

Validation

↓

Accepted

Registration completes only after all required accounts are received.

---

Stage 6 — Training Assignment

After successful registration:

The worker receives training resources.

Resources include:

- Account Setup Video
- Upload Tutorial
- Bio Text
- Telegram Invite Link
- Assigned Profile Photos
- Audio

Global resources remain common.

Worker resources remain unique.

---

Stage 7 — Account Setup

The worker completes Instagram setup.

Tasks include:

- Profile photo
- Bio text
- Telegram invite link
- Other required configuration

The system does not assume completion.

Verification is required.

---

Stage 8 — Setup Verification

The worker submits setup screenshots.

The number of screenshots equals the number of required Instagram accounts.

Example:

1 Account

↓

1 Screenshot

2 Accounts

↓

2 Screenshots

3 Accounts

↓

3 Screenshots

Screenshots are collected sequentially.

The worker never sees internal account mappings.

---

Stage 9 — Worker Activation

After setup submission:

The worker becomes eligible for work.

The system enables:

- Dashboard
- History
- Training Center
- Work Assignment
- Weekly Reward

The worker officially becomes Active.

---

Stage 10 — Slot Configuration

The worker selects preferred working slots.

The administrator defines:

- Minimum daily slots
- Maximum daily slots

The worker chooses:

- Preferred time
- Number of slots

Workers may modify their schedule according to platform rules.

---

Stage 11 — Waiting State

Until the next scheduled slot:

The worker remains idle.

The Dashboard displays:

- Next Work Time
- Current Status
- Weekly Reward Status

---

Stage 12 — Work Assignment

At slot time:

The system performs:

1. Previous work cleanup
2. Sends work package
3. Sends caption
4. Starts deadline timer

Work packages include:

- Assigned reels
- Caption
- Instructions

---

Stage 13 — Work Completion

The worker uploads assigned reels.

After finishing:

The worker selects:

«Submit Work»

The system requests screenshots.

The number of screenshots remains dynamic.

---

Stage 14 — Screenshot Submission

The worker submits screenshots one by one.

Example:

Screenshot 1

↓

Accepted

↓

Screenshot 2

↓

Accepted

↓

Submission Complete

Worker interaction remains simple.

Internal mapping remains hidden.

---

Stage 15 — Review Queue

Submitted work enters the Screenshot Review Queue.

Possible outcomes:

- Pending
- Approved
- Rejected

Worker continues receiving future work regardless of review status unless administrative rules block assignments.

---

Stage 16 — Daily Continuation

The worker waits for the next slot.

The cycle repeats:

Receive Work

↓

Upload

↓

Submit

↓

Next Slot

---

Stage 17 — Weekly Review

At the end of each Season:

Administrators review:

- Completed Work
- Missed Work
- Rejected Work
- Overall Performance

---

Stage 18 — Weekly Reward

After administrative review:

The worker receives:

- Weekly Reward
- Bonus (if applicable)

Before approval:

The worker only sees:

Weekly Reward

Locked 🔒

Available after weekly review.

---

Stage 19 — New Season

A new Season begins.

The worker continues working without repeating onboarding.

---

Additional Worker States

Vacation Mode

Workers may temporarily pause work.

During Vacation:

- No work assignments
- Profile remains active
- Progress preserved

After Vacation:

The worker resumes normally.

---

Temporary Schedule Change

Workers may temporarily modify schedules according to platform rules.

Original schedule remains recoverable.

---

Extra Work

Workers may manually request additional work.

Rules:

- Allowed only if scheduling conditions are satisfied.
- Administrator settings determine eligibility.

---

Instagram Account Replacement

Workers may request account replacement.

Reasons include:

- Ban
- Login Problem
- Disabled
- Other

Replacement does not restart worker registration.

Only affected account data changes.

---

Training Revisit

Workers may reopen Training Center anytime.

They always receive:

Current assigned worker resources.

Latest approved global resources.

---

Support

Workers may contact administrators through Support.

Support conversations remain separate from technical bug reports.

---

Bug Report

Workers may submit:

- Description
- Screenshot (optional)

Reports enter the Bug Workspace.

---

Maintenance Mode

If maintenance is enabled:

Workers receive maintenance information.

No normal operations continue until maintenance ends.

---

Appeal

Removed workers may submit an appeal if enabled.

Appeals are reviewed by administrators.

If approved:

Worker resumes previous progress.

---

Migration

If the platform migrates to another bot:

The worker starts the new bot.

The system restores:

- Worker Profile
- Training
- Accounts
- Progress
- Current Status

The worker continues from the previous state.

---

Permanent Removal

If administrators permanently delete a worker:

Worker resources are removed according to project policy.

Only the minimum audit record remains.

The lifecycle ends permanently.

---

Worker State Diagram

Registered

↓

Training

↓

Setup

↓

Active

↓

Working

↓

Weekly Review

↓

Weekly Reward

↓

Working

↓

Working

↓

Vacation

↓

Working

↓

Account Change

↓

Working

↓

Migration

↓

Working

↓

Removed

↓

Appeal (Optional)

↓

Working

OR

Deleted

---

Lifecycle Rules

The following rules always apply.

- Worker identity never changes.
- Worker experience remains simple.
- Instagram accounts may change.
- Work never requires repeating onboarding.
- History must remain preserved.
- Automation supports administrators.
- High-risk actions remain auditable.
- Worker progress should always continue unless explicitly stopped.

---

Final Statement

The Worker Lifecycle defines the complete journey of every worker within IWMS.

Every user-facing screen, workflow, automation rule, notification, and administrative action must align with the lifecycle defined in this document.

Any future feature affecting worker behavior must update this lifecycle before implementation.

---

End of Document
