37_Database_Schema.md

«Document Version: 1.0
Status: Approved
Module: Database Schema
Priority: Critical»

---

Purpose

The Database Schema defines the logical data structure of the Instagram Workforce Management System (IWMS).

It establishes how every resource is organized, related, validated, and maintained while ensuring scalability, consistency, and data integrity.

This document defines the logical architecture, not a specific database technology.

---

Philosophy

The database is the single source of truth.

Every resource owns its own data.

Resources communicate through references rather than duplicating information.

---

Design Principles

The schema must be:

- Modular
- Normalized
- Scalable
- Consistent
- Recoverable
- Extensible

Business logic should never depend on physical storage implementation.

---

Database Architecture

Database

│

├── Core Resources

├── Operational Resources

├── Administrative Resources

├── System Resources

└── Infrastructure Resources

---

Core Resources

Core business resources:

- Worker
- Instagram
- Training
- Channel Link
- Profile Photos

These resources define worker identity and assignments.

---

Operational Resources

Operational resources include:

- Slot
- Work
- Screenshot
- Review
- Weekly Reward
- Notification
- Season

---

Administrative Resources

Administrative resources include:

- Administrator
- Permission
- Support
- Bug Report

---

System Resources

System resources include:

- Timeline
- Audit
- Logging
- Health Reports
- Search Index
- Backup Metadata
- Migration History

---

Infrastructure Resources

Infrastructure resources include:

- Automation Jobs
- Scheduled Events
- Media Library
- Configuration
- Version Information

---

Primary Relationships

Worker
│
├── Instagram
├── Training
├── Slot
├── Work
│      │
│      ├── Screenshot
│      └── Review
│
├── Weekly Reward
├── Support
├── Bug Report
├── Timeline
└── Audit

Every Worker is the root of operational data.

---

Resource Ownership

Each resource owns only its own data.

Example:

Worker Resource owns:

- Worker identity
- Worker status

It does NOT own:

- Reviews
- Screenshots
- Rewards

---

Reference Rules

Resources communicate using IDs.

Example:

Worker ID

↓

WK-00154

↓

Referenced by:

Work

Review

Reward

Timeline

Objects should never be embedded inside other objects.

---

Primary Keys

Every resource has one immutable primary identifier.

Examples:

WK-000001

WRK-000001

REV-000001

SUP-000001

BUG-000001

IDs never change after creation.

---

Foreign References

Resources reference each other using permanent IDs.

Example:

Work

↓

Worker ID

Season ID

Training ID

Instagram ID

Broken references are considered integrity failures.

---

Normalization Rules

The schema follows these principles:

- No duplicate worker data
- No duplicate media
- No duplicate reward calculations
- No duplicate review metadata

Shared information must be referenced.

---

Resource Isolation

Every module stores only its own information.

Example:

Review Resource stores:

- Decision
- Reviewer
- Notes

It does NOT store:

- Screenshot files
- Worker profile
- Reward information

---

Data Consistency

Every write operation should ensure:

- Valid references
- Valid states
- Unique IDs
- Integrity checks

Invalid writes should be rejected.

---

Transactions

Critical operations should execute atomically.

Examples:

- Worker removal
- Migration
- Season closure
- Reward approval

Either all related updates succeed or none are committed.

---

Soft Delete Policy

Operational resources should generally use soft deletion.

Example:

Status

↓

Removed

↓

Archived

↓

Hidden

Permanent deletion is reserved for maintenance policies.

---

Versioning

Version-controlled resources include:

- Training
- Media
- Configuration
- Bot Version
- Database Version

Historical versions remain available.

---

Indexing Strategy

Recommended indexes:

- Resource IDs
- Telegram User IDs
- Instagram Usernames
- Status
- Season ID
- Date
- Administrator ID

Indexes improve search performance.

---

Data Integrity Rules

The database should enforce:

- Unique IDs
- Valid references
- Valid state transitions
- Mandatory fields
- Version compatibility

---

Security Rules

Sensitive information should be isolated.

Examples:

- Permissions
- Audit
- Logs
- Administrator Sessions

Workers must never access protected tables.

---

Backup Compatibility

Every resource should support:

- Export
- Backup
- Restore
- Migration

No resource should require manual reconstruction.

---

Timeline Integration

Business resources create Timeline entries.

Timeline does not own business data.

---

Audit Integration

Sensitive operations create Audit records.

Audit stores change history only.

---

Health Check Integration

The Health Check validates:

- References
- IDs
- Relationships
- Missing resources
- Corrupted records

---

Performance Guidelines

The schema should:

- Minimize duplication
- Use references
- Keep resources independent
- Optimize read-heavy operations
- Support future scaling

---

Resource Relationships

Core Resources
        │
        ▼
Operational Resources
        │
        ▼
Administrative Resources
        │
        ▼
System Resources
        │
        ▼
Infrastructure Resources

---

Future Expansion

Supports:

- Distributed databases
- Read replicas
- Sharding
- Multi-region deployment
- Analytics warehouse
- Event sourcing

---

Database Overview

Worker
Instagram
Training
ChannelLink
ProfilePhoto
Slot
Work
Screenshot
Review
Reward
Notification
Season
Support
BugReport
Admin
Permission
Timeline
Audit
Logging
Health
Migration
Backup
Media
Automation
Scheduler
Search
Configuration

Each resource remains logically independent.

---

Edge Cases

- Duplicate ID generation.
- Broken foreign references.
- Partial migration.
- Interrupted transaction.
- Simultaneous updates.
- Historical version restoration.

---

Validation Checklist

Before committing data:

- Primary ID valid.
- References valid.
- State valid.
- Required fields complete.
- Integrity checks passed.

---

Implementation Checklist

- Resource schema
- Primary IDs
- Foreign references
- Integrity validation
- Transactions
- Soft deletion
- Versioning
- Indexing
- Backup compatibility

---

TPY Implementation Notes

- TPY resources should reference each other using permanent IDs instead of duplicating data.
- Validation should occur before every write operation.
- Shared utilities should handle ID generation and integrity checks.
- Database access should be abstracted behind resource modules wherever possible.

---

Final Statement

The Database Schema is the official logical data model of IWMS.

It defines how every resource is organized, connected, validated, and maintained, ensuring long-term scalability, consistency, modularity, and compatibility with every operational and administrative component of the platform.

---

End of 37_Database_Schema.md
