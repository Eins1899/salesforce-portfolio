# OWN Archive — Authenticated User Setup

## Overview
This document covers the setup of the dedicated 
OWN Archive Backup Integration User required to 
connect the OWN Archive application to Salesforce.

## Environment
- Production Org: samw@ramtracking.com
- Sandbox: ram--fullsb.sandbox.lightning.force.com
- OWN Account: einstein.amazu@klipboard.com
- Region: uk1

## Profile Created
- Name: OWN - Archive Backup Integration
- Cloned from: System Administrator
- Description: Cloned from System Administrator. 
  Dedicated integration profile for OWN Archive 
  and Backup authenticated user. Do not modify 
  without consulting the Salesforce Administrator. 
  Created June 2026.

## User Created
- Name: OWN Archive Backup Integration User
- Username (Production): 
  own.archivebackup.integration@ramtracking.com
- Username (Full Sandbox): 
  own.archivebackup.integration@ramtracking.com.fullsb
- Nickname (Production): OWNArchiveBackup-PRD
- Nickname (Full Sandbox): OWNArchiveBackup-FSB
- Licence: Salesforce (Full)
- Profile: OWN - Archive Backup Integration
- Email: operations@ramtracking.com

## Permission Sets Assigned
| Permission Set | Purpose |
|---|---|
| Archive Admin | Comprehensive Archive management |
| Archive Analyzer | Create/edit/delete archive policies |
| Archive Policy Permission | Create purge policies |

## Profile System Permissions Enabled
| Permission | Purpose |
|---|---|
| API Enabled | Access Salesforce API |
| Bulk API Hard Delete | Permanently delete records, bypass Recycle Bin |

## Org Level Settings Enabled
Location: Setup → User Interface
- Set Audit Fields upon Record Creation ✅
- Update Records with Inactive Owners ✅

## Notes
- Salesforce Integration User licence is NOT 
  compatible with Archive — full Salesforce 
  licence required
- Do not use personal user accounts to authenticate 
  OWN services — always use this dedicated user
- Created: June 2026
- Created by: Einstein Amazu
