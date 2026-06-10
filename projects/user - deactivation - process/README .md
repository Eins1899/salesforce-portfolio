# User Licence Hygiene — Monthly Inactive User Deactivation Process

![Type: Admin](https://img.shields.io/badge/Type-Admin-green)
![Status: In Progress](https://img.shields.io/badge/Status-In%20Progress-orange)
![Cadence: Monthly](https://img.shields.io/badge/Cadence-Monthly-blue)
![Year: 2025](https://img.shields.io/badge/Year-2025-lightgrey)

## The problem

Salesforce user licences are a recurring cost. Without a regular review process, inactive users — leavers, role changes, or staff who simply stopped using the platform — continue consuming licences and represent a security risk through dormant active accounts.

The organisation had no formalised process for identifying and deactivating inactive users. This project establishes a repeatable monthly workflow to address that.

---

## Objectives

- Identify all active Salesforce users who have not logged in within the past 30 days
- Surface users who have never logged in since account creation
- Route findings to line managers and stakeholders for verification
- Deactivate confirmed leavers in bulk via CSV upload
- Integrate with the existing Leavers process for downstream steps
- Maintain a clear audit trail of every deactivation decision

---

## What I built and delivered

### 1. SOQL query library
Two SOQL queries written and tested via Salesforce Inspector to extract the relevant user data from the production org:

**Query 1 — Users with no login in the past 30 days:**
```sql
SELECT
  Id,
  FirstName,
  LastName,
  Username,
  Email,
  Profile.Name,
  UserRole.Name,
  LastLoginDate,
  CreatedDate,
  IsActive
FROM User
WHERE IsActive = true
AND LastLoginDate < LAST_N_DAYS:30
AND Profile.Name != 'Chatter Free User'
ORDER BY LastLoginDate ASC NULLS LAST
```

**Query 2 — Users who have never logged in:**
```sql
SELECT
  Id,
  FirstName,
  LastName,
  Username,
  Email,
  Profile.Name,
  CreatedDate,
  IsActive
FROM User
WHERE IsActive = true
AND LastLoginDate = null
AND Profile.Name != 'Chatter Free User'
ORDER BY CreatedDate ASC
```

> Note: Two separate queries are required because `NULL` values do not satisfy date comparisons in SOQL — users who have never logged in will not appear in Query 1.

---

### 2. Stakeholder review spreadsheet template
A structured Excel template for routing findings to line managers and stakeholders, including:

- All query output fields
- A `Recommended Action` column with standardised values: `Deactivate`, `Keep — New Starter`, `Keep — On Leave`, `Escalate`
- A `Confirmed By` column for sign-off tracking
- A `Date Confirmed` column for audit trail purposes

---

### 3. Bulk deactivation CSV format
A standardised two-column CSV format for bulk user deactivation via Salesforce Inspector or Data Loader:

```csv
Id,IsActive
0052w000000XXXXX,false
0052w000000YYYYY,false
```

Setting `IsActive = false` immediately revokes login access and frees the Salesforce licence for reallocation.

---

### 4. End-to-end process documentation
A documented monthly process covering:

- When to run (first working day of each month)
- How to run both SOQL queries and export results
- How to clean and prepare the stakeholder review file
- Sign-off SLA — stakeholders given 3–5 working days to respond
- How to prepare and upload the deactivation CSV
- Handoff point to the existing Leavers process
- Where to file audit evidence (OneNote — private, not in this repo)

---

## Process overview

```
Run SOQL queries (Salesforce Inspector)
        ↓
Export results → clean in Excel
(remove integration/system/API users)
        ↓
Add Recommended Action column
        ↓
Send to line manager + stakeholders for sign-off
(3–5 working day SLA)
        ↓
Prepare deactivation CSV (confirmed leavers only)
        ↓
Bulk update via Inspector/Data Loader (IsActive = false)
        ↓
Verify deactivation → re-run query to confirm
        ↓
Follow existing Leavers process
        ↓
File audit trail in OneNote
```

---

## Key decisions and guardrails

**Users never deactivated regardless of login date:**
- Integration users and API-only accounts
- System/automation accounts
- Scheduled job owners
- Salesforce admin accounts
- Users created within the last 30 days (new starters)

**Why `Profile.Name` matters:**
Filtering by profile is the fastest way to identify system accounts before the review reaches stakeholders — it prevents accidental deactivation of accounts that would break integrations or automations.

**Why the audit trail is non-negotiable:**
Deactivating a user is irreversible in the short term and can have downstream impacts (record ownership, approval processes, queue membership). Every deactivation must be backed by a named approver and a date.

---

## Skills demonstrated

`SOQL` `Salesforce Inspector` `Data Loader` `User Management` `Licence Management` `Security & Access` `Process Design` `Stakeholder Management` `Data Export & Import` `Audit & Compliance` `Documentation`

---

## Outcome

*(To be updated on completion of first run)* — Expected outcomes:
- Reduction in number of active licences consumed by inactive users
- Documented, repeatable monthly process owned by the Salesforce Admin team
- Audit trail in place for all deactivation decisions
- Integration with existing Leavers process formalised

---

## Artefacts in this folder

| File | Description |
|---|---|
| `soql/inactive-users-30-days.soql` | Query 1 — users with no login in 30+ days |
| `soql/never-logged-in-users.soql` | Query 2 — users who have never logged in |
| `docs/process-guide.md` | Step-by-step monthly process documentation |
| `docs/stakeholder-review-template.md` | Review spreadsheet column definitions |
| `docs/deactivation-csv-format.md` | CSV format reference for bulk deactivation |

---

## Related processes

- Leavers Process *(internal — not in this repo)*
- OwnBackup Implementation *(see [`../ownbackup-implementation`](../ownbackup-implementation/))*

---

*First run scheduled: next month. README will be updated with real outcomes and any process refinements following the initial run.*
