28_Admin_System.md

«Document Version: 1.0
Status: Approved
Module: Admin System
Priority: Critical»

---

Purpose

The Admin System manages all administrative users, responsibilities, operational tools, and privileged actions within the Instagram Workforce Management System (IWMS).

It provides a secure environment where administrators can efficiently manage workers, resources, reviews, rewards, and system operations without interfering with each other's responsibilities.

---

Philosophy

Administrators are operators, not owners.

Every administrator should receive only the permissions required for their assigned responsibilities.

All administrative actions must be:

- Authorized
- Logged
- Audited
- Traceable
- Recoverable

---

Responsibilities

The Admin System manages:

- Administrator registration
- Administrator roles
- Responsibility assignment
- Administrative dashboard
- Administrative actions
- Session management
- Timeline integration
- Audit integration

It does not manage:

- Permissions (Permission System)
- Worker resources
- Business logic
- Automation

---

Ownership

Primary Owner:

Admin Module

---

Administrator Types

Supported administrator types:

- Super Admin
- Secondary Admin
- Read-Only Admin (Optional)
- System Administrator (Future)

Each administrator has exactly one primary role.

---

Primary Fields

Field| Description
Admin ID| Permanent identifier
Telegram User ID| Telegram account
Role| Administrator role
Display Name| Administrator name
Status| Active/Inactive
Assigned Responsibilities| Managed modules
Last Login| Last activity
Session Status| Current session

---

Administrator Identity

Every administrator receives a permanent identifier.

Example:

ADM-000001

ADM-000002

ADM-000003

Administrator IDs never change.

---

Administrator States

Supported states:

- Pending
- Active
- Suspended
- Removed

Only Active administrators may perform administrative actions.

---

Administrative Dashboard

The dashboard provides quick access to:

- Pending Reviews
- Support Tickets
- Bug Reports
- Worker Search
- Reward Management
- System Status
- Pending Approvals
- Notifications
- Logs

Dashboard widgets should respect assigned permissions.

---

Responsibility Assignment

A Secondary Admin may be responsible for:

- Screenshot Reviews
- Support Tickets
- Bug Reports
- Worker Management
- Rewards
- Broadcasts
- Training Resources
- Instagram Resources

Responsibilities are independent from roles.

---

Administrative Groups

The system uses dedicated Telegram groups/channels.

Examples:

Review Group

Support Group

Bug Report Group

Log Channel

Approval Group

Announcement Channel

Each workspace has a dedicated purpose.

---

Administrative Sessions

Every administrator has a managed session.

Session information includes:

- Login Time
- Last Activity
- Active Device (future)
- Session Status

Inactive sessions may expire automatically.

---

Worker Management

Authorized administrators may:

- View workers
- Search workers
- Suspend workers
- Restore workers
- Replace resources
- Open worker timeline

Worker removal requires Super Admin approval.

---

Dual Confirmation Integration

Critical actions require approval.

Examples:

- Worker removal
- Season closure
- Migration
- Permission changes
- System reset
- Reward override

Workflow:

Admin

↓

Request

↓

Approval Group

↓

Super Admin

↓

Approve

↓

Execute

---

Temporary Responsibilities

Responsibilities may be assigned temporarily.

Example:

Review Access

↓

48 Hours

↓

Automatically Removed

---

Timeline Integration

Timeline events include:

- Administrator Added
- Administrator Suspended
- Responsibility Assigned
- Responsibility Removed
- Login
- Logout

---

Audit Integration

Administrative actions always generate Audit records.

Examples:

- Worker changes
- Reward changes
- Permission changes
- Configuration updates
- Resource replacements

---

Search Support

Search by:

- Admin ID
- Telegram User ID
- Role
- Responsibility
- Status

Results should provide:

- Admin Profile
- Audit History
- Timeline
- Assigned Responsibilities

---

Security Rules

Administrators:

- Must be verified.
- Must pass permission checks.
- Must have active sessions.
- Must be audited.

Administrative sessions should expire after inactivity.

---

Administrator Permissions

The Admin System delegates permission validation to the Permission System.

It never performs authorization independently.

---

Archive Policy

Removed administrators remain archived.

Historical records remain available for:

- Audit
- Timeline
- Security investigations

Administrator history must never be deleted.

---

Backup Policy

Backups preserve:

- Administrator profiles
- Roles
- Responsibilities
- Sessions
- References

---

Health Check

The Health Checker verifies:

- Duplicate Admin IDs
- Invalid roles
- Broken permissions
- Expired sessions
- Missing responsibilities

---

Performance Guidelines

The Admin System stores:

- Identity
- Responsibilities
- References

Operational business data remains in dedicated resources.

---

Resource Relationships

Admin System
      │
      ├── Permission System
      ├── Worker Resource
      ├── Review Resource
      ├── Support Resource
      ├── Bug Report Resource
      ├── Timeline
      └── Audit

---

Field Classification

Identity

- Admin ID
- Telegram User ID

---

Configuration

- Role
- Responsibilities
- Status

---

Metadata

- Created Time
- Last Login
- Last Activity

---

Future Expansion

Supports:

- Multi-device sessions
- Multi-factor authentication
- Department hierarchy
- Regional administrators
- AI workload balancing
- Administrator performance analytics

---

Database Schema Summary

Administrator

│

├── Admin ID

├── Telegram User ID

├── Role

├── Responsibilities

├── Status

├── Session

├── Timeline Reference

└── Audit Reference

---

Edge Cases

- Administrator removed while handling reviews.
- Session expires during an operation.
- Two administrators edit the same worker simultaneously.
- Responsibility transferred to another administrator.
- Telegram username changes.

---

Validation Checklist

Before allowing an administrative operation:

- Administrator exists.
- Session active.
- Account active.
- Permission granted.
- Dual confirmation completed (if required).

---

Implementation Checklist

- Admin ID generation
- Session management
- Dashboard
- Responsibility assignment
- Search
- Timeline integration
- Audit logging
- Approval workflow

---

TPY Implementation Notes

- Every admin command should begin with session and permission validation.
- Separate administrative groups should be configurable through resources rather than hard-coded IDs.
- Dashboard widgets should load dynamically based on permissions.
- Critical actions must invoke the Dual Confirmation workflow before execution.

---

Final Statement

The Admin System is the official administrative management framework for IWMS.

It provides secure administrator management, responsibility assignment, centralized operational tools, dedicated workspaces, and complete integration with the Permission, Timeline, and Audit systems while ensuring scalability, accountability, and operational security.

---

End of 28_Admin_System.md
