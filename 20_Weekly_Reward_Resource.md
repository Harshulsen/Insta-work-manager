20_Weekly_Reward_Resource.md

«Document Version: 1.0
Status: Approved
Module: Weekly Reward Resource
Priority: Critical»

---

Purpose

The Weekly Reward Resource manages weekly worker performance, reward eligibility, payment tracking, and season-based earnings within the Instagram Workforce Management System (IWMS).

It determines who deserves a reward, why, and how much, while keeping reward calculations transparent and auditable.

---

Philosophy

Workers are rewarded based on verified work, not assigned work.

Only approved work contributes toward rewards.

Every reward calculation must be:

- Fair
- Transparent
- Traceable
- Repeatable
- Auditable

---

Responsibilities

The Weekly Reward Resource manages:

- Weekly performance
- Reward eligibility
- Reward calculations
- Payment status
- Reward history
- Season summaries
- Timeline integration
- Audit integration

It does not manage:

- Work assignments
- Screenshot reviews
- Worker identity
- Payment gateway integration

---

Ownership

Primary Owner:

Weekly Reward Module

---

Resource Lifetime

Property| Value
Created| At season start
Updated| After every approved/rejected work
Closed| At season end
Archived| After payout
Deleted| Never

---

Reward Philosophy

Each worker has one Weekly Reward Resource for each season.

Example:

Worker WK-154

↓

Season S-2026-W28

↓

Reward Resource

One worker can therefore have many historical reward resources.

---

Reward Identity

Every reward receives a permanent identifier.

Example:

RWD-000001

RWD-000002

RWD-000003

Reward IDs never change.

---

Primary Fields

Field| Description
Reward ID| Permanent identifier
Worker ID| Parent Worker
Season ID| Related season
Approved Work| Total approved work
Rejected Work| Total rejected work
Missed Work| Total missed work
Completion Rate| Calculated value
Reward Status| Current status
Payment Status| Current payment state
Reward Amount| Calculated amount

---

Reward Lifecycle

Season Started

↓

Statistics Updated

↓

Eligibility Check

↓

Reward Calculated

↓

Payment Approved

↓

Payment Sent

↓

Archived

---

Reward Status

Supported values:

- Collecting
- Eligible
- Ineligible
- Calculated
- Approved
- Paid
- Archived

---

Payment Status

Supported values:

- Pending
- Processing
- Completed
- Failed
- Cancelled

Payment status is independent from reward eligibility.

---

Statistics Source

Statistics come from verified resources only.

Sources:

- Approved Work
- Rejected Work
- Missed Work

Manual edits should be exceptional and audited.

---

Reward Calculation

The calculation engine should use:

- Approved work count
- Bonus rules
- Penalty rules
- Season configuration

The formula itself should remain configurable.

The Weekly Reward Resource stores only the final result.

---

Eligibility Rules

Workers become eligible only if they satisfy project rules.

Examples:

- Minimum approved work reached.
- No disqualifying violations.
- Season completed.
- Worker active.

The exact rules remain configurable.

---

Bonus Support

Future bonus categories:

- Perfect Week
- High Accuracy
- Zero Missed Work
- Campaign Bonus
- Festival Bonus

Bonuses should remain modular.

---

Penalty Support

Possible penalties:

- Missed work
- Repeated rejection
- Rule violations
- Manual deductions

Penalties should always generate Timeline and Audit records.

---

Timeline Integration

Timeline events include:

- Reward Created
- Eligibility Updated
- Reward Calculated
- Payment Approved
- Payment Completed
- Bonus Added
- Penalty Applied

---

Audit Integration

Audit required for:

- Manual reward adjustment
- Manual payment approval
- Bonus override
- Penalty override
- Payment correction

Audit includes:

- Administrator
- Timestamp
- Reward ID
- Worker ID
- Reason

---

Season Integration

Every reward belongs to one season.

Season

↓

Weekly Reward

↓

Worker

Closing a season automatically archives its rewards.

---

Search Support

Search by:

- Reward ID
- Worker ID
- Season ID
- Payment Status
- Reward Status

Results should allow:

- Open Worker Profile
- Open Season Summary
- Open Payment Details
- Open Timeline

---

Security Rules

Workers may:

- View current reward progress.
- View payment status.
- View reward history.

Workers may not:

- Modify calculations.
- Change payment status.
- View administrative adjustments.

---

Administrator Permissions

Action| Secondary Admin| Super Admin
View Reward| ✅| ✅
Calculate Reward| Optional| ✅
Approve Payment| ❌| ✅
Manual Adjustment| ❌| ✅
Archive Reward| ❌| ✅

---

Archive Policy

Archived rewards remain available for:

- Worker History
- Reports
- Timeline
- Audit
- Migration

Archived rewards are read-only.

---

Backup Policy

Backups preserve:

- Statistics
- Reward Amount
- Payment Status
- Timeline References
- Audit References

---

Health Check

The Health Checker verifies:

- Existing Worker
- Existing Season
- Statistics consistency
- Reward calculation integrity
- Payment status validity

---

Performance Guidelines

The Weekly Reward Resource stores:

- Calculated values
- Metadata
- References

It should never duplicate:

- Work Resources
- Screenshot Resources
- Review Resources

---

Resource Relationships

Worker Resource
        │
        ▼
Weekly Reward Resource
        │
        ├── Season Resource
        ├── Work Resource
        ├── Review Resource
        ├── Timeline
        └── Audit

---

Field Classification

Identity

- Reward ID
- Worker ID
- Season ID

---

Current Configuration

- Reward Status
- Payment Status
- Reward Amount

---

Statistics

- Approved Work
- Rejected Work
- Missed Work
- Completion Rate

---

Metadata

- Created Date
- Calculated Date
- Paid Date

---

Future Expansion

Supports:

- Multi-level bonus system
- Referral rewards
- Achievement rewards
- Monthly rewards
- Leaderboards
- AI fraud detection
- Multiple payment methods

---

Database Schema Summary

Weekly Reward

│

├── Reward ID

├── Worker ID

├── Season ID

├── Statistics

├── Reward Amount

├── Payment Status

├── Timeline Reference

└── Audit Reference

---

Edge Cases

- Worker removed before payout.
- Season reopened.
- Payment fails after approval.
- Manual reward correction.
- Worker restored after deletion.
- Reward recalculated due to administrative review.

---

Validation Checklist

Before approving payment:

- Worker exists.
- Season closed.
- Reward calculated.
- No pending reviews.
- Payment information available.
- Administrator authorized.

---

Implementation Checklist

- Reward ID generation
- Statistics aggregation
- Eligibility engine
- Reward calculation
- Payment tracking
- Timeline integration
- Audit logging
- Season archive
- Search indexing

---

TPY Implementation Notes

- Reward calculations should use aggregated statistics from Work and Review resources.
- Business rules must remain configurable rather than hard-coded.
- Payment processing should be implemented through a dedicated Payment Module, not inside this resource.
- Reward recalculation should always create an audit entry.

---

Final Statement

The Weekly Reward Resource is the official specification for reward and payment management within IWMS.

Every reward calculation, eligibility decision, payment approval, and historical record must comply with this architecture.

Future enhancements should extend this specification while maintaining compatibility with the Work, Review, Season, Timeline, and Audit resources.

---

End of 20_Weekly_Reward_Resource.md
