# BambooHR Integration Specification

## Purpose
Sync employee data from BambooHR to LeaveFlow to ensure:
- New hires are automatically provisioned with correct leave balances
- Level/role changes update leave entitlements
- Departures deactivate the user (history is preserved for audit)

## Sync Schedule
- Full sync: nightly at 02:00 AM
- Delta sync (changes only): every 4 hours during business hours (08:00–18:00)

## Field Mapping
| BambooHR Field   | LeaveFlow Field  |
|------------------|------------------|
| employeeId       | externalId       |
| firstName        | firstName        |
| lastName         | lastName         |
| jobLevel         | employeeLevel    |
| managerId        | managerId        |
| hireDate         | joiningDate      |
| terminationDate  | deactivatedAt    |
| department       | department       |

## Business Rules
- If employee level changes, annual balance is recalculated pro-rata for current year on next sync
- If terminationDate is set, user is deactivated — pending requests are automatically cancelled
- New employees receive a welcome email from LeaveFlow on first sync

## Error Handling
- If BambooHR API is unavailable: skip and retry at next scheduled run
- Sync errors are logged and visible in HR Admin → Integrations panel
- Three consecutive sync failures trigger an alert email to the System Admin