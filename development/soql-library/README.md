# SOQL Library

A reference collection of useful SOQL queries built and used across projects.
All queries use generic object/field names — substitute your org's API names as needed.

---

### Open opportunities by owner this quarter

```sql
SELECT OwnerId, Owner.Name, COUNT(Id) oppCount, SUM(Amount) totalValue
FROM Opportunity
WHERE StageName != 'Closed Won'
AND StageName != 'Closed Lost'
AND CloseDate = THIS_QUARTER
GROUP BY OwnerId, Owner.Name
ORDER BY totalValue DESC
```

---

### Accounts with no activity in 90 days

```sql
SELECT Id, Name, LastActivityDate, OwnerId
FROM Account
WHERE LastActivityDate < LAST_N_DAYS:90
OR LastActivityDate = null
ORDER BY LastActivityDate ASC NULLS FIRST
```

---

### Leads created this month not yet converted

```sql
SELECT Id, Name, Company, CreatedDate, OwnerId
FROM Lead
WHERE IsConverted = false
AND CreatedDate = THIS_MONTH
ORDER BY CreatedDate DESC
```
