24_Support_Resource.md

«Document Version: 1.0
Status: Approved
Module: Support Resource
Priority: Critical»

---

Purpose

The Support Resource manages every support conversation between workers and administrators within the Instagram Workforce Management System (IWMS).

Its objective is to provide a structured ticketing system instead of allowing support requests to clutter the administrator's private bot chat.

Every worker issue should be tracked until resolution.

---

Philosophy

Support is a conversation, not a message.

One issue creates one Support Ticket.

Every future reply belongs to the same ticket until it is resolved.

---

Responsibilities

The Support Resource manages:

- Support ticket creation
- Conversation tracking
- Status management
- Admin assignment
- Reply history
- Resolution tracking
- Timeline integration
- Audit integration

It does not manage:

- Bug reports
- Worker performance
- Work review
- Rewards

---

Ownership

Primary Owner:

Support Module

---

Resource Lifetime

Property| Value
Created| When worker opens a support request
Updated| Whenever a reply is added
Resolved| After administrator closes the issue
Archived| After retention period
Deleted| Never (except retention policy)

---

Support Philosophy

Every problem should have exactly one ticket.

Example:

Worker

↓

Support Ticket

↓

Conversation

↓

Resolved

A new issue requires a new ticket.

---

Support Identity

Every ticket receives a permanent identifier.

Example:

SUP-000001

SUP-000002

SUP-000003

Ticket IDs never change.

---

Primary Fields

Field| Description
Support ID| Permanent identifier
Worker ID| Ticket owner
Assigned Admin| Current administrator
Status| Current ticket status
Category| Support category
Priority| Ticket priority
Created Time| Ticket creation
Last Reply| Latest activity

---

Ticket Categories

Supported categories:

- Account Issue
- Training Question
- Work Issue
- Screenshot Issue
- Reward Question
- Technical Problem
- General Help
- Other

Categories help routing and reporting.

---

Ticket Priorities

Supported priorities:

- Low
- Normal
- High
- Critical

Priority affects administrator attention but does not change ticket identity.

---

Ticket Status

Supported states:

- Open
- Waiting for Worker
- Waiting for Admin
- In Progress
- Resolved
- Closed
- Archived

Only one active status exists.

---

Ticket Workflow

Worker

↓

Create Ticket

↓

Support Group

↓

Admin Assigned

↓

Conversation

↓

Resolved

↓

Closed

---

Support Group Integration

All support tickets should appear in a dedicated Telegram Support Group.

The bot should:

- Post the ticket.
- Thread replies (if supported) or logically group them.
- Allow administrators to reply directly from the group.

Workers should continue communicating only with the bot.

The bot acts as the bridge.

---

Conversation History

Every reply should be preserved.

History includes:

- Sender
- Timestamp
- Message Type
- Attachments
- Delivery Status

Conversation history must never be overwritten.

---

Attachments

Support messages may contain:

- Text
- Photos
- Documents
- Voice Messages
- Videos

All attachments remain linked to the same Support Ticket.

---

Administrator Assignment

Tickets may be:

- Automatically assigned
- Manually assigned
- Claimed by an administrator (future)

Only one administrator should actively manage a ticket at a time.

---

Timeline Integration

Timeline events include:

- Ticket Created
- Admin Assigned
- Reply Added
- Ticket Resolved
- Ticket Closed
- Ticket Reopened

---

Audit Integration

Audit required for:

- Ticket reassignment
- Forced closure
- Priority override
- Status override
- Manual deletion (if ever permitted)

---

Search Support

Search by:

- Support ID
- Worker ID
- Administrator
- Status
- Category

Results should allow:

- Open Worker Profile
- Open Conversation
- Open Timeline

---

Worker Permissions

Workers may:

- Open tickets.
- Reply.
- Upload attachments.
- View ticket status.
- Close their own ticket (optional).

Workers may not:

- Delete conversations.
- Edit administrator replies.

---

Administrator Permissions

Action| Secondary Admin| Super Admin
View Ticket| ✅| ✅
Reply| Optional| ✅
Assign Ticket| Optional| ✅
Change Priority| ❌| ✅
Force Close| ❌| ✅

---

Archive Policy

Resolved tickets become archived after the configured retention period.

Archived tickets remain available for:

- Timeline
- Audit
- Worker History
- Reports

---

Backup Policy

Backups preserve:

- Ticket Metadata
- Conversation History
- Attachments
- References

---

Health Check

The Health Checker verifies:

- Existing Worker
- Existing Administrator
- Broken attachments
- Invalid status
- Orphaned tickets

---

Performance Guidelines

Store:

- References
- Metadata
- Conversation

Avoid duplicating Worker or Timeline data.

---

Resource Relationships

Worker Resource
        │
        ▼
Support Resource
        │
        ├── Support Group
        ├── Timeline
        ├── Audit
        └── Notification

---

Field Classification

Identity

- Support ID
- Worker ID

---

Configuration

- Status
- Category
- Priority
- Assigned Admin

---

Metadata

- Created Time
- Last Reply
- Closed Time

---

Future Expansion

Supports:

- AI-assisted replies
- Suggested solutions
- FAQ integration
- Ticket templates
- Satisfaction ratings
- Automatic routing
- Multi-language support

---

Database Schema Summary

Support Ticket

│

├── Support ID

├── Worker ID

├── Assigned Admin

├── Category

├── Status

├── Conversation

├── Timeline Reference

└── Audit Reference

---

Edge Cases

- Worker blocks the bot.
- Administrator leaves the support group.
- Ticket reopened after closure.
- Duplicate ticket for the same issue.
- Large attachment uploads.
- Worker removed while ticket is open.

---

Validation Checklist

Before creating a ticket:

- Worker exists.
- Worker is allowed to use support.
- Category selected.
- Initial message received.
- Ticket ID generated.

---

Implementation Checklist

- Ticket ID generation
- Support group integration
- Conversation bridge
- Attachment support
- Admin assignment
- Timeline integration
- Audit logging
- Archive handling
- Search indexing

---

TPY Implementation Notes

- The worker should never communicate directly with administrators.
- The bot must relay messages between the worker and the Support Group.
- Store Telegram message IDs to support replies and future synchronization.
- Keep conversation history append-only.

---

Final Statement

The Support Resource is the official specification for worker support management within IWMS.

Every support request, reply, attachment, assignment, and resolution must follow this architecture, ensuring organized communication, complete history, administrator accountability, and seamless integration with the Timeline, Notification, and Audit resources.

---

End of 24_Support_Resource.md
