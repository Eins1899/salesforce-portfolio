# OwnBackup Implementation — Data & Metadata Backup Strategy

![Type: Admin](https://img.shields.io/badge/Type-Admin-green)
![Status: In Progress](https://img.shields.io/badge/Status-In%20Progress-orange)
![Tool: OwnBackup](https://img.shields.io/badge/Tool-OwnBackup-00A1E0?style=flat)
![Year: 2025](https://img.shields.io/badge/Year-2026-blue)

## The problem

The organisation had no formal backup and archiving strategy in place for its Salesforce environment. A structured solution was needed to protect both data and metadata across environments, with clear policies governing retention, frequency, and scope.

## What I was asked to deliver

- Connect and configure OwnBackup across Salesforce environments
- Establish a backup strategy covering both data and metadata
- Produce a formal backup policy document for stakeholder sign-off
- Define a naming convention to ensure consistency across all backup services

---

## What I built and delivered

### 1. Sandbox connection and testing
Connected OwnBackup to the Salesforce sandbox environment to validate the tool's behaviour before any production configuration. Used the sandbox as a controlled environment to understand the archive dialogue, service setup, and backup job behaviour.

### 2. Metadata backup configuration
Configured a dedicated metadata backup service alongside the data backup — ensuring configuration, customisations, flows, and schema changes are protected independently of record-level data. This distinction matters: losing metadata can be more damaging than losing data, as it affects the entire org's functionality.

### 3. Naming convention
Defined and documented a naming convention for all backup services to ensure consistency and clarity as the number of backup jobs grows:

```
[Organisation Name] - [Environment] - [Org Name or ID] - [Type: Data or Metadata]
```

**Example:**
```
Acme Corp - Production - 00D000000000001 - Data
Acme Corp - Production - 00D000000000001 - Metadata
Acme Corp - Sandbox - DevSandbox - Data
Acme Corp - Sandbox - DevSandbox - Metadata
```

This convention makes it immediately clear — without opening a job — what org, environment, and content type each backup service covers.

### 4. Backup policy document
Produced a formal backup policy document covering:

- **Frequency** — how often backups run (daily / weekly / on-demand)
- **Retention period** — how long backup snapshots are kept before expiry
- **Scope** — which objects, fields, and metadata types are included
- **Environments covered** — production and sandbox distinctions

Document is currently awaiting stakeholder sign-off.

---

## Challenges and current status

### Blocker — sandbox not appearing in archive dialogue
During initial setup, the sandbox environment was not appearing in OwnBackup's archive dialogue box as a selectable service. This prevented the archiving configuration from being completed.

**Action taken:** Raised a formal support ticket with OwnBackup's technical team documenting the issue in full — expected behaviour, actual behaviour, steps already taken, and environment details. A support meeting has been scheduled and is yet to take place.

**Current status:** Implementation paused on archiving configuration pending OwnBackup support resolution. All other deliverables (metadata backup, naming convention, policy document) are complete or in review.

---

## Skills demonstrated

`OwnBackup` `Backup & Recovery Strategy` `Metadata Management` `Sandbox Administration` `Policy Documentation` `Third-Party Tool Integration` `Vendor Escalation` `Naming Conventions`

## Outcome

*(To be updated on completion)* — Target outcome is a fully configured, documented backup and archiving solution covering data and metadata across all Salesforce environments, with a signed-off policy and consistent naming convention in place for ongoing management.

---

## Lessons learned so far

- Sandbox environments can behave differently from production in third-party tools — always validate connectivity in sandbox first, but never assume sandbox parity
- Distinguishing between **data backup** and **metadata backup** is a conversation worth having early with stakeholders — most assume backup means records only
- A clear naming convention is worth defining before creating a single backup job — retrofitting it later is painful
- When a third-party tool misbehaves, raising a structured support ticket early with clear reproduction steps gets faster resolution than chasing informally

---

## Artefacts in this folder

- `docs/naming-convention.md` — naming convention reference guide
- `docs/backup-policy.md` — backup policy document (anonymised, to be added on sign-off)
- `docs/support-ticket.md` — anonymised support ticket raised with OwnBackup (to be added post-resolution)

# OWN Backup & Archive Implementation

## Overview
This project documents the implementation of OWN 
(Own from Salesforce) Backup and Archive at 
RAM Tracking, covering setup, configuration, 
and ongoing management.

## Project Status
- Backup: ✅ Live in Production since April 2022
- Archive: ✅ Configured and tested in Sandbox
- Archive Production rollout: ⏳ Pending approval

## Key Stats (June 2026)
- Records backed up: 287,973,220
- Data size: 361.83 GB
- Files backed up: 2,554,827
- Data storage usage: 246% of limit

## Documentation
| Document | Description |
|---|---|
| naming-convention.md | OWN service naming standards |
| authenticated-user-setup.md | Dedicated integration user setup |
| sandbox-setup.md | Full Sandbox archive configuration |
| archive-policy-notes.md | Archive candidates and policy notes |

## Related
- Salesforce Data Archiving Policy — SharePoint
- Personal Development Plan — SharePoint

## Author
Einstein Amazu — Salesforce Administrator
RAM Tracking — June 2026

*This project is ongoing. README will be updated as the implementation progresses and the support issue is resolved.*
