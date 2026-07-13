36_Global_Media_Library.md

«Document Version: 1.0
Status: Approved
Module: Global Media Library
Priority: Critical»

---

Purpose

The Global Media Library (GML) is the centralized repository for all reusable media assets used throughout the Instagram Workforce Management System (IWMS).

Instead of storing duplicate copies inside multiple resources, every reusable media file is stored once and referenced wherever required.

The Global Media Library is the platform's single source of truth for media assets.

---

Philosophy

Media belongs to the platform.

Resources only store references.

A media file should never be duplicated simply because multiple workers use it.

---

Responsibilities

The Global Media Library manages:

- Training videos
- Profile photos
- Tutorial videos
- Audio files
- Bio captions
- Bio links
- Screenshot templates
- Welcome media
- Announcement media
- Future reusable assets

It does not manage:

- Worker progress
- Work assignments
- Reviews
- Rewards

---

Ownership

Primary Owner:

Media Library Module

---

Core Principles

The Media Library must be:

- Centralized
- Versioned
- Searchable
- Reusable
- Lightweight
- Immutable after publication

---

Media Categories

Supported categories:

- Training Video
- Upload Tutorial
- Audio
- Profile Photo
- Bio Caption
- Bio Link
- Welcome Message
- Announcement
- Screenshot Template
- Other

New categories may be added without redesign.

---

Media Identity

Every media asset receives a permanent identifier.

Example:

MED-000001

MED-000002

MED-000003

Media IDs never change.

---

Media Versions

Media assets support versioning.

Example:

Training Video

↓

V1

↓

V2

↓

V3

Workers always receive the version assigned to them.

Updating a resource creates a new version rather than modifying the existing one.

---

Resource References

Resources store only Media IDs.

Example:

Training Resource

↓

MED-0012

────────────

Profile Photo Pack

↓

MED-0041

MED-0042

MED-0043

The actual file exists only once.

---

Assignment Philosophy

There are two assignment models:

Global Assignment

Same media for everyone.

Examples:

- Training Video
- Upload Tutorial
- Audio
- Bio Caption

---

Individual Assignment

Different media per worker.

Examples:

- Profile Photos
- Instagram Accounts
- Invite Links

The assigned Media ID is stored inside the related resource.

---

Media Status

Supported states:

- Draft
- Active
- Deprecated
- Archived

Only Active media may be assigned.

---

Media Lifecycle

Upload

↓

Validation

↓

Published

↓

Assigned

↓

Archived

Published media should remain immutable.

---

Version Compatibility

Workers always continue using the version originally assigned unless an administrator explicitly replaces it.

This guarantees consistent training and account setup.

---

Timeline Integration

Timeline events include:

- Media Uploaded
- Media Published
- Media Assigned
- Media Replaced
- Media Archived

---

Audit Integration

Audit records required for:

- Media replacement
- Media removal
- Version publication
- Manual reassignment

---

Search Support

Search by:

- Media ID
- Category
- Version
- Status
- File Name

Results should provide:

- Media Details
- Assigned Resources
- Assignment History

---

Security Rules

Workers may access only media assigned to them.

Workers may never browse the complete Media Library.

Only administrators manage media assets.

---

Administrator Permissions

Action| Secondary Admin| Super Admin
View Media| ✅| ✅
Upload Media| Optional| ✅
Publish Version| ❌| ✅
Archive Media| ❌| ✅
Delete Media| ❌| ❌

Published media should never be permanently deleted.

---

Archive Policy

Archived media remains available for:

- Historical training
- Timeline
- Audit
- Migration

Archived media cannot be assigned to new workers.

---

Backup Policy

Backups preserve:

- Media metadata
- Version history
- Resource references
- Assignment history

Telegram media references should also be backed up.

---

Health Check

The Health Check verifies:

- Missing media
- Broken media references
- Duplicate Media IDs
- Invalid versions
- Missing assignments

---

Performance Guidelines

Resources should store only Media IDs.

The Media Library should manage all reusable files to eliminate duplication.

---

Resource Relationships

Global Media Library
        │
        ├── Training Resource
        ├── Profile Photos Resource
        ├── Work Resource
        ├── Notification Resource
        ├── Timeline
        └── Audit

---

Future Expansion

Supports:

- AI media tagging
- Automatic compression
- Multi-language assets
- CDN integration
- Usage analytics
- Expiration policies

---

Database Schema Summary

Media

│

├── Media ID

├── Category

├── Version

├── Status

├── Telegram File Reference

├── Timeline Reference

└── Audit Reference

---

Edge Cases

- Telegram file becomes unavailable.
- Media version rollback.
- Duplicate upload.
- Resource references archived media.
- Media replaced during active training.

---

Validation Checklist

Before publishing media:

- Media uploaded.
- Category assigned.
- Version unique.
- Validation complete.
- Media ID generated.

---

Implementation Checklist

- Media ID generation
- Version management
- Assignment references
- Search indexing
- Timeline integration
- Audit logging
- Archive handling
- Backup support

---

TPY Implementation Notes

- Store Telegram "file_id" (or equivalent media reference) instead of downloading media.
- All reusable media should be referenced by Media ID.
- Never duplicate media across resources.
- Media replacement should create a new version rather than modifying existing assignments.

---

Final Statement

The Global Media Library is the official media repository of IWMS.

Every reusable file, training asset, profile photo, tutorial, caption, and media resource must be managed through this library, ensuring centralized storage, version control, efficient reuse, and seamless integration across the entire platform.

---

End of 36_Global_Media_Library.md
