# Lead Conversion Automation

![Type: Admin](https://img.shields.io/badge/Type-Admin-green)
![Complexity: Medium](https://img.shields.io/badge/Complexity-Medium-yellow)
![Year: 2025](https://img.shields.io/badge/Year-2025-blue)

## The problem

A mid-size B2B company was manually reassigning leads to account owners after conversion — a daily task taking ~45 minutes and prone to errors when territories overlapped.

## What I built

- Record-triggered Flow firing on Lead conversion, auto-assigning the resulting Opportunity to the correct Account owner based on territory field logic
- Validation rule preventing conversion unless mandatory qualification fields were completed
- Email alert notifying the assigned owner immediately on conversion

## Skills demonstrated

`Flow Builder` `Record-Triggered Flows` `Validation Rules` `Email Alerts` `Formula Fields`

## Outcome

Eliminated ~45 minutes of daily manual reassignment. Error rate on territory assignment dropped to zero in the first month post-deployment.

## Artefacts in this folder

- `flows/` — exported Flow XML (anonymised)
- `screenshots/` — anonymised UI screenshots of the Flow canvas

## Notes

Considered using an Apex trigger for the assignment logic but Flow covered all requirements without code — simpler to maintain for the admin team long-term. Tested across 3 sandbox environments before production deployment.
