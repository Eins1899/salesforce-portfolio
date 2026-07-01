# OWN Archive — Archive Policy Notes

## Overview
This document covers the archive policy 
configuration and key considerations for 
RAM Tracking's Salesforce data archiving 
strategy using OWN Archive.

## Business Context
- Salesforce Data Storage: 246% of limit
- Salesforce File Storage: 39% of limit
- Licence renewal approaching
- Archiving required to reduce storage costs

## Archive Candidates — Priority Order

| Priority | Object | Criteria | Est. Impact |
|---|---|---|---|
| 1 | Files & Attachments | Older than 2 years | High |
| 2 | Cases | Closed > 2 years | High |
| 3 | Messages | Created > 2 years | High |
| 4 | Interaction Events | Created > 2 years | High |
| 5 | Interaction Event Notes | Created > 2 years | High |
| 6 | Email Messages | Created > 2 years | High |
| 7 | Opportunities | Closed Lost > 3 years | Medium |
| 8 | Activities | Completed > 2 years | Medium |
| 9 | Usage Stats | Created > 1 year | Medium |
| 10 | Custom Objects | TBC with business | TBC |

## Key Storage Statistics (June 2026)
| Object | Records | Storage |
|---|---|---|
| Tasks | 11,535,061 | 21.9 GB |
| Transaction Line Items | 8,149,492 | 15.5 GB |
| Deliveries | 7,750,728 | 14.8 GB |
| Messages | 6,244,079 | 11.9 GB |
| Interaction Events | 5,752,498 | 11.0 GB |
| Interaction Event Notes | 5,752,498 | 11.0 GB |
| Email Messages | 1,773,231 | 9.1 GB |
| Usage Stats | 1,443,853 | 2.8 GB |

## ⚠️ Object Relationship Warning
When archiving — always archive parent and 
child objects together:

| Parent | Child | Note |
|---|---|---|
| Interaction Events | Interaction Event Notes | Archive together always |
| Cases | Case Comments | Archive together always |
| Opportunities | Opportunity Line Items | Archive together always |

Archiving parent without child records will 
break relationships on unarchiving.

## Archive Policy Configuration
- Archive policies configured in OWN Archive app
- Tested in Full Sandbox (FullSB) before Production
- Unarchive/recovery process tested and verified

## Unarchiving Process
1. Log into app.owndata.com
2. Click Find tab
3. Search for record by name/ID/object
4. View record in OWN — no storage impact
5. Click Unarchive to restore to Salesforce
6. Note: Unarchived records count against 
   storage again

## Compliance Considerations
- Data stored in AWS UK (uk1 region) — GDPR 
  compliant
- Right to Erasure requests can be actioned 
  on archived records via OWN
- Minimum retention periods to be confirmed 
  with Legal team
- See full Archiving Policy document for 
  complete compliance details

## Next Steps
- Get archive policies signed off by management
- Run archive policies in Production
- Monitor storage reduction
- Report results ahead of licence renewal
- Consider upgrading Production from 
  v24.24 to v24.32

## Related Documents
- RAM Tracking Salesforce Data Archiving 
  Policy (Word document — see SharePoint)
- authenticated-user-setup.md
- sandbox-setup.md
- naming-convention.md

## Notes
- Created: June 2026
- Created by: Einstein Amazu
- Status: Sandbox tested — awaiting 
  Production rollout approval


  ## Archive Policies Created — June 2026

### Policy 1 — Archive Completed Tasks 2Y+
| Setting | Value |
|---|---|
| **Object** | Tasks__c |
| **Query** | Status__c = Completed AND CreatedDate < 2 years |
| **Schedule** | Daily 02:00 AM UTC |
| **Limit** | 10,000 per run |
| **Retention** | 3 years |
| **Protection** | 90 days |
| **Child Objects** | None |
| **Environment** | Full Sandbox (FullSB) |
| **Status** | ✅ Created and running |

### Policy 2 — Archive Cancelled Orders 2Y+
| Setting | Value |
|---|---|
| **Object** | Order__c |
| **Query** | Order_Status__c IN (Cancelled statuses) AND CreatedDate < 2 years |
| **Schedule** | Daily 02:00 AM UTC |
| **Limit** | 10,000 per run |
| **Retention** | 3 years |
| **Protection** | 90 days |
| **Child Objects** | Order_Contract__c (via Order__c lookup) |
| **Environment** | Full Sandbox (FullSB) |
| **Status** | ✅ Created — awaiting manager sign-off for Production |

### Policy 3 — Archive Cancelled Engineer Bookings 2Y+
| Setting | Value |
|---|---|
| **Object** | Service_Booking__c (Engineer Booking in OWN) |
| **Query** | Marked_as_Cancelled_Date__c != null AND CreatedDate < 2 years |
| **Schedule** | Daily 02:00 AM UTC |
| **Limit** | 10,000 per run |
| **Retention** | 3 years |
| **Protection** | 90 days |
| **Child Objects** | None (Invoice_Service_Booking__c field deprecated) |
| **Environment** | Full Sandbox (FullSB) |
| **Status** | ✅ Created — awaiting manager sign-off for Production |

## Key Technical Discoveries

| Discovery | Detail |
|---|---|
| Tasks__c vs Task | The business Tracking uses custom Tasks__c not standard Task object |
| Service_Booking__c | Displays as "Engineer Booking" in OWN Archive dropdown |
| FinancialForce objects | fferpcore, ffbc, c2g, ffrr, ffct namespaces — need FF sign-off before archiving |
| Invoice_Service_Booking__c | Junction object — Service Booking field deprecated (_del suffix) |
| Manual query mode | Required for date filters in OWN — LIMIT must be included in SOQL |
| Order_Contract__c | Child of Order__c — 51,027 records — archive together with orders |

## Policies Pending Sign-Off

| Policy | Object | Blocker |
|---|---|---|
| Completed Orders | Order__c | Manager sign-off needed |
| Invoiced Orders | Order__c | Finance confirmation needed |
| FinancialForce Objects | fferpcore/ffbc/c2g | FF support sign-off needed |
| Engineer Booking Completed | Service_Booking__c | Manager sign-off needed |

## Storage Impact Estimate (Sandbox)

| Policy | Eligible Records |
|---|---|
| Tasks | 223 (Sandbox) / millions (Production) |
| Cancelled Orders | 29,318 |
| Cancelled Engineer Bookings | 9,933 |
| **Total so far** | **~39,474** |
