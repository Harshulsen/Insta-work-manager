02_Business_Model.md

«Document Version: 1.0
Status: Approved
Module: Business Architecture
Priority: Critical»

---

Purpose

This document explains the business model of the Instagram Workforce Management System (IWMS).

Unlike technical documents, this file focuses on how the business operates, how workers interact with the platform, and why each workflow exists.

Every technical implementation must follow the business rules defined here.

---

Business Overview

IWMS is a Telegram-based workforce management platform that distributes Instagram-related work to registered workers.

Workers perform tasks using their own Instagram accounts.

The platform manages:

- Worker onboarding
- Worker training
- Work assignment
- Submission
- Review
- Weekly rewards
- Worker management

The entire system is designed to operate through Telegram.

---

Business Goal

The goal of the platform is to build a structured workforce capable of completing Instagram-related tasks while maintaining:

- consistent quality
- organized management
- scalable operations
- simple worker experience

The platform should be capable of managing thousands of workers simultaneously.

---

Core Philosophy

The business follows one fundamental rule.

«Workers perform work.»

«Administrators manage workers.»

«The system manages everything else.»

Workers should never manually manage complex workflows.

---

Worker Lifecycle

Every worker follows the same lifecycle.

Discover Bot

↓

Apply

↓

Select Language

↓

Submit Instagram Accounts

↓

Training

↓

Account Setup

↓

Verification

↓

Receive Work

↓

Submit Screenshots

↓

Weekly Review

↓

Weekly Reward

↓

Continue Working

This lifecycle repeats continuously.

---

Worker Recruitment

Workers join the platform through the Telegram bot.

After joining:

- language selection
- Instagram account submission
- account setup
- training

No work is assigned before onboarding is completed.

---

Worker Identity

Every worker receives a permanent identity.

The identity remains constant even if:

- Instagram accounts change
- profile photos change
- invite links change
- bot version changes

Worker identity is independent of Instagram accounts.

---

Instagram Accounts

Instagram accounts are temporary business assets.

Accounts may change due to:

- bans
- restrictions
- login issues
- worker requests
- administrator decisions

The system must support unlimited account replacements throughout a worker's lifetime.

---

Account Setup

Workers configure their Instagram accounts using resources provided by the system.

Training resources include:

- Setup Video
- Upload Tutorial
- Bio Text
- Telegram Invite Link
- Profile Photos
- Audio

Some resources are global.

Some resources are worker-specific.

---

Training Philosophy

Training is not a one-time event.

Workers should always be able to reopen the Training Center.

Whenever training is reopened:

Worker-specific resources remain identical unless changed by an administrator.

Global resources always display the latest approved version.

---

Work Distribution

The system distributes work automatically.

Workers receive:

- Reel Package
- Caption
- Deadline

The worker uploads all assigned reels.

After completion:

The worker submits screenshots.

---

Slot-Based Operation

The platform operates using worker-selected time slots.

Workers choose:

- preferred working hours
- number of daily slots

Administrators define:

- minimum slots
- maximum slots
- slot rules

Workers may request additional work outside their normal schedule if platform rules allow.

---

Daily Work Cycle

Each work slot follows the same lifecycle.

Previous Work Cleanup

↓

New Work Sent

↓

Worker Uploads

↓

Worker Submits Screenshots

↓

Next Slot

Previous work messages should be cleaned before new work is delivered.

---

Missed Work

Every work assignment has a deadline.

If screenshots are not submitted before the next slot deadline:

The assignment becomes:

Missed Work.

The worker continues receiving future work unless restricted by administrative rules.

---

Screenshot Submission

Screenshot submission exists for work verification.

The number of screenshots depends on the number of required Instagram accounts.

Examples:

1 Instagram Account

↓

1 Screenshot

2 Instagram Accounts

↓

2 Screenshots

3 Instagram Accounts

↓

3 Screenshots

The process remains dynamic.

---

Work Review

Submitting screenshots does not automatically approve work.

Every submission enters the review queue.

Administrators review:

Approve

Reject

Request Changes (future support)

Approval determines reward eligibility.

---

Weekly Reward Philosophy

Workers never receive payment immediately after completing work.

Instead:

All work contributes toward the weekly review.

At the end of the week:

Administrators review worker performance.

Rewards become available only after approval.

---

Hidden Reward Model

Workers should never see estimated earnings.

Instead they see:

Weekly Reward

Locked 🔒

Available after weekly review.

This prevents reward expectations before administrative review.

---

Bonus System

Administrators may assign bonuses.

Bonuses remain completely manual.

Possible reasons include:

- excellent performance
- consistency
- special contribution
- campaign completion

Bonus values remain hidden until weekly approval.

---

Worker Levels

Every worker belongs to a level.

Examples:

- Bronze
- Silver
- Gold
- Platinum

Levels represent worker performance.

Levels are not direct payment values.

---

Seasons

One business week equals one season.

Each season represents:

- work completed
- reviews
- reward
- level progress

A new season begins every week.

---

Work Continuity

Workers should continue receiving work regardless of review completion.

Pending review must never block future work unless administrators explicitly configure restrictions.

---

Channel Link Assignment

Every worker receives a unique Telegram invite link.

The link is used inside Instagram.

Administrators may:

- regenerate links
- restore previous links
- reuse previous links

Every version remains documented.

---

Profile Photos

Workers receive assigned profile photos.

Assignment is random by default.

The number of assigned photos always equals the number of required Instagram accounts.

Photos remain assigned until changed.

---

Resource Ownership

Business resources belong to one of two categories.

Global Resources

Shared by everyone.

Examples:

- Setup Video
- Upload Tutorial
- Bio Text
- Audio

---

Worker Resources

Unique for each worker.

Examples:

- Invite Link
- Profile Photos
- Instagram Accounts
- Slots
- Language

---

Worker Dashboard

The dashboard is the worker's primary interface.

It should provide:

- Current Work
- Weekly Reward Status
- Training
- History
- Profile
- Support

Workers should never navigate through unnecessary menus.

---

Worker History

Workers should always be able to review:

- completed work
- missed work
- approved work
- pending work

History exists for transparency.

---

Support System

Workers may contact administrators through the support system.

Communication always starts from the worker.

Administrators respond through dedicated workspaces.

---

Bug Reports

Workers may submit:

- description
- optional screenshot

Bug reports are routed to a dedicated technical workspace.

---

Worker Removal

Administrators may:

Pause

Remove

Delete

Each action has different business consequences.

Appeal availability is configurable.

---

Migration Philosophy

If the platform moves to a new bot:

Workers should continue exactly where they stopped.

Migration should never require restarting the onboarding process.

---

Administrative Philosophy

Administrators exist to supervise workers.

The system exists to automate repetitive work.

Automation should reduce manual effort while preserving administrative control.

---

Business Success Metrics

The platform evaluates success through:

- Worker Activity
- Work Completion Rate
- Approval Rate
- Worker Retention
- Review Speed
- Weekly Productivity
- System Stability

Revenue calculations are intentionally excluded from worker visibility.

---

Long-Term Vision

The project is designed to evolve beyond a Telegram bot.

The architecture should eventually support:

- Multiple campaigns
- Multiple task types
- AI-assisted review
- External dashboards
- Enterprise-scale workforce management

without redesigning the business model.

---

Final Statement

The business model defined in this document is considered the official operational foundation of the project.

Every database resource, automation engine, admin panel, and implementation must support these business rules.

If future requirements conflict with this document, the business rules must be reviewed before implementation.

---

End of Document
