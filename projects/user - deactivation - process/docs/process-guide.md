# Monthly Inactive User Deactivation — Process Guide

## When to run
First working day of each month, against the production org.

## Step-by-step

### 1. Run the SOQL queries
Open Salesforce Inspector in Chrome → SOQL tab.
Run both queries from the `soql/` folder. Export each as CSV.

### 2. Clean the export in Excel
- Combine both CSV exports into one sheet
- Remove any integration users, API users, or system accounts
  (check Profile.Name — flag anything that looks automated)
- Remove any users created within the last 30 days (new starters)
- Add the following columns:
  - `Recommended Action` — values: Deactivate / Keep — New Starter / Keep — On Leave / Escalate
  - `Confirmed By` — name of approving stakeholder
  - `Date Confirmed` — date sign-off received

### 3. Send to stakeholders
Email the spreadsheet to line manager and relevant stakeholders.
Give a clear response deadline — 3 to 5 working days.
Document who you sent it to and when.

### 4. Prepare deactivation CSV
Once sign-off received, filter to rows marked `Deactivate`.
Create a new CSV with two columns only:

```
Id,IsActive
[User Id],[false]
```

### 5. Upload via Salesforce Inspector
Inspector → Data Import → Object: User → Operation: Update
Upload CSV → map Id to Id, IsActive to IsActive → run.

### 6. Verify
Re-run Query 1. Deactivated users should no longer appear.
Spot-check 2 or 3 users in the Salesforce UI to confirm IsActive = false.

### 7. Follow Leavers process
Hand off to the existing Leavers process for record reassignment,
queue removal, and any other downstream steps.

### 8. File audit trail
Save the following in OneNote (private — not in this repo):
- Signed-off stakeholder spreadsheet
- Deactivation CSV used
- Name and date of each approver
- Screenshot of post-deactivation query confirming changes
