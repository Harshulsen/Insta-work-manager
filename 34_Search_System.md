34_Search_System.md

«Document Version: 1.0
Status: Approved
Module: Search System
Priority: Critical»

---

Purpose

The Search System provides a centralized search engine for every resource inside the Instagram Workforce Management System (IWMS).

Its objective is to allow administrators to instantly locate any worker, work assignment, screenshot, review, reward, support ticket, bug report, timeline entry, audit record, or system resource using multiple search methods.

The Search System is the official information retrieval framework of IWMS.

---

Philosophy

Search should never modify data.

It should only retrieve and present the most relevant information as quickly as possible.

The Search System must provide fast, consistent, and permission-aware results.

---

Responsibilities

The Search System manages:

- Global search
- Resource search
- Cross-resource search
- Search indexing
- Advanced filters
- Search history
- Permission-aware visibility
- Search analytics

It does not manage:

- Business logic
- Resource ownership
- Permissions
- Timeline generation

---

Ownership

Primary Owner:

Search Module

---

Core Principles

The Search System must be:

- Fast
- Accurate
- Permission-aware
- Scalable
- Consistent
- Extensible

---

Search Scope

The Search System supports searching:

- Workers
- Instagram Accounts
- Training Resources
- Profile Photos
- Channel Links
- Work Resources
- Screenshot Resources
- Review Resources
- Weekly Rewards
- Notifications
- Timeline
- Audit
- Support Tickets
- Bug Reports
- Seasons
- Administrators

---

Search Methods

Supported methods:

- ID Search
- Name Search
- Username Search
- Telegram User ID
- Instagram Username
- Date Range
- Status
- Category
- Tags (Future)

---

Global Search

Global Search simultaneously searches all indexed resources.

Example:

WK-154

↓

Worker

↓

Related Work

↓

Reviews

↓

Timeline

↓

Support Tickets

The system should group results by resource type.

---

Resource Search

Administrators may search a specific resource only.

Examples:

- Worker Search
- Review Search
- Screenshot Search
- Reward Search
- Timeline Search

---

Search Workflow

Search Query

↓

Permission Check

↓

Search Index

↓

Matching Resources

↓

Sorted Results

↓

Administrator

---

Search Index

Every searchable resource should maintain an index.

Indexed fields include:

- IDs
- Names
- Usernames
- Status
- Categories
- Dates
- Relationships

Large media files are not indexed.

---

Search Results

Each result should display:

- Resource Type
- Resource ID
- Primary Information
- Current Status
- Last Updated
- Quick Actions

Example:

Worker

WK-154

Status: Active

Open Profile

---

Advanced Filters

Supported filters:

- Status
- Date
- Administrator
- Worker
- Season
- Priority
- Category

Filters may be combined.

---

Related Resources

Results should display related resources.

Example:

Worker

↓

Work

↓

Reviews

↓

Rewards

↓

Timeline

This reduces navigation time.

---

Search History

Administrators may view recent searches.

History includes:

- Query
- Timestamp
- Administrator

Search history should respect privacy settings.

---

Permission Awareness

Search results must always respect permissions.

Example:

A Screenshot Reviewer should not see:

- Reward Management
- Permission Settings
- Migration Records

Unauthorized resources should never appear.

---

Timeline Integration

Timeline events include:

- Manual Search (Optional)
- Search Analytics (Optional)

Routine searches should generally not clutter the Timeline.

---

Audit Integration

Audit records required for:

- Exported search results
- Sensitive search categories
- Administrative investigations

Normal searches should not generate Audit records unless configured.

---

Search Performance

Search should:

- Use indexes
- Minimize full scans
- Cache frequent lookups
- Return results incrementally

---

Search Ranking

Results should prioritize:

1. Exact ID match
2. Exact username match
3. Exact name match
4. Partial match
5. Related resources

---

Search Suggestions

Future support:

- Auto-complete
- Recent searches
- Popular searches
- AI suggestions

---

Security Rules

The Search System must:

- Validate administrator permissions.
- Hide unauthorized resources.
- Prevent data leakage.
- Respect archived resource policies.

---

Administrator Permissions

Action| Secondary Admin| Super Admin
Search Assigned Resources| ✅| ✅
Global Search| Optional| ✅
Export Results| ❌| ✅
Search Audit Records| ❌| ✅

---

Archive Policy

Archived resources remain searchable if permissions allow.

Archived status should be clearly indicated.

---

Health Check

The Health Check verifies:

- Broken indexes
- Missing indexed resources
- Duplicate index entries
- Search performance degradation

---

Resource Relationships

Search System
        │
        ├── Worker Resource
        ├── Work Resource
        ├── Timeline
        ├── Audit
        ├── Support
        ├── Bug Reports
        └── All Indexed Resources

---

Future Expansion

Supports:

- Full-text search
- Semantic search
- AI-powered search
- OCR search
- Image similarity search
- Saved searches
- Smart filters

---

Database Schema Summary

Search Index

│

├── Resource Type

├── Resource ID

├── Indexed Fields

├── Status

├── Last Indexed

└── Permission Scope

---

Edge Cases

- Duplicate usernames.
- Resource deleted after indexing.
- Partial migration.
- Broken references.
- Large result sets.
- Concurrent indexing.

---

Validation Checklist

Before returning results:

- User authorized.
- Index available.
- Resource exists.
- Result not hidden.
- Related references valid.

---

Implementation Checklist

- Global search
- Resource search
- Index manager
- Permission filter
- Related resource lookup
- Advanced filters
- Search history
- Performance monitoring

---

TPY Implementation Notes

- Maintain lightweight indexes rather than scanning every resource.
- Apply permission filtering before displaying results.
- Support direct ID lookup for fast administrative workflows.
- Rebuild indexes automatically after major migrations or restores.

---

Final Statement

The Search System is the official information retrieval framework of IWMS.

It enables administrators to locate any authorized resource quickly and securely while maintaining permission-aware visibility, scalable indexing, and seamless integration across the entire platform.

---

End of 34_Search_System.md
