# LeaveFlow — Test Data Guide

## Annual Leave Allocation by Level
- Junior: 20 days
- Mid: 22 days
- Senior: 25 days
- Manager: 25 days

## Test Users (staging environment)
| Name              | Email                              | Role      | Level   | Total | Used | Pending | Available |
|-------------------|------------------------------------|-----------|---------|-------|------|---------|-----------|
| Ana Popescu       | ana.popescu@leaveflow.test         | Employee  | Mid     | 22    | 10   | 0       | 12        |
| Mihai Ionescu     | mihai.ionescu@leaveflow.test       | Manager   | Manager | 25    | 8    | 5       | 12        |
| Ioana Dumitrescu  | ioana.dumitrescu@leaveflow.test    | HR Admin  | Senior  | 25    | 3    | 0       | 22        |
| Radu Constantin   | radu.constantin@leaveflow.test     | Employee  | Junior  | 20    | 14   | 0       | 6         |

## Key Edge Case Scenarios
- Insufficient balance: Radu has 6 days left — any request above 6 days should be blocked
- Manager self-request: Mihai's own requests should route to HR, not back to himself
- Public holiday overlap: any request that spans August 15 should not count that day as a working day
- Pending conflict: Ana has a pending request for Aug 4–8 (5 days) — overlapping requests should warn
- Pro-rated balance: a new employee joining July 1 should receive 50% of annual entitlement
- Carry-over expiry: days carried from last year expire March 31 — requests after that date use only current-year balance