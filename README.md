# entra-manual-access-review
## Overview

## Project Purpose
Create a "manual access review package" in **Microsoft Entra ID** by validating user access (group membership) against a **role-to-group source-of-truth matrix**.

## What this demonstrates
- IAM fundamentals (least privilege, access governance)
- Manual access review workflow when automated reviews (Entra ID P2 license) are unavailable
- Clear documentation: findings, risk statements, recommendations, and evidence

  ## Lab environment (setup)
  ### Groups created
  -'HR-App-Users'
  -'Contractors'
  -'IT-Admins'

  ### Users created
  -'test.user1'
  -'test.user2'
  -'test.user3'
  -'test.user4'
  -'test.user5'
  -'test.user6'
  -'test.user7'
  -'test.user8'

## Review method
See: [Manual access review procedure](docs/01-manual-access-review-procedure.md)

## Role-to-Group Access Matrix (source of truth)
| Role/Title | Division | Expected Entra Group(s) | Notes/Justification |
|---|---|---|---|
| HR Coordinator / Talent Acquisition | HR | HR-App-Users | Access to HR app |
| Contractor (e.g., Cleaning, Electrician, Landscape) | Contractor | Contractors | Limited access |
| IT Admin | IT | IT-Admins | Privileged admin tasks |
| Vendor (e.g., Outsource Market) | Vendor | Contractors | Treat vendors as contractors in this lab |

## User-to-Role Mapping
| User | Role/Title | Division |
|---|---|---|
| test.user1 | HR Coordinator | HR |
| test.user2 | Cleaning contractor | Contractor |
| test.user3 | Electrician | Contractor |
| test.user4 | Talent Acquisition | HR |
| test.user5 | IT Trainee | IT |
| test.user6 | Outsource Market | Vendor |
| test.user7 | Equipment Technician | IT |
| test.user8 | Landscape | Contractor |

## Findings summary (recommendations only — pending approval)
Two users were found to be mismatched to the role-to-group matrix.
| User | Current group | Expected group | Risk / Why it matters | Recommendation | Status | Evidence |
|---|---|---|---|---|---|---|
| `test.user3` | `IT-Admins` | `Contractors` | Excess privilege: contractor has access intended for IT admins. Compromise could impact admin-level resources. | Remove from `IT-Admins`; add to `Contractors` | Pending approval | `evidence/it-admins.png` |
| `test.user7` | `HR-App-Users` | `IT-Admins` | Incorrect access assignment: user may lack required IT access and has unnecessary HR app access. | Remove from `HR-App-Users`; add to `IT-Admins` | Pending approval | `evidence/hr-app-users.png` |
See details: [Findings and recommendations](docs/02-findings-and-recommendations.md)

## Evidence
### `test.user3` — IT-Admins membership
![it-admins evidence](./evidence/it-admins.png)

### `test.user7` — HR-App-Users membership
![hr-app-users evidence](./evidence/hr-app-users.png)

## Assumptions / limitations
- Entra ID P2 was not available, so access reviews were performed manually.
- For lab simplicity, all IT roles are mapped to `IT-Admins`.
- In a real environment, IT access would be separated into standard IT groups vs privileged admin groups.
- No changes were implemented in this lab; findings are documented as recommendations pending approval.

## How to reproduce this review 
(1) Prerequisites
You have access to the target Microsoft Entra tenant.
You have permission to view Users, Groups, and Directory roles (at minimum).
You have the scope of the review defined (which roles, which groups, which apps, and the review period).

(2) Set the review scope 
Review date:
Roles in scope (e.g., Global Administrator, User Administrator, etc.):
Groups in scope (security groups / M365 groups used for access):
Apps/resources in scope (if applicable):

(3) Collect current directory role assignments
Go to Entra admin center → Roles & admins.
For each role in scope:
Open the role → Assignments / Assigned roles.
Record who is assigned (user/service principal if visible), and whether it looks direct or via an eligible process (if your tenant supports it).
Take a screenshot for evidence.

(4) Collect group membership evidence
Go to Entra admin center → Groups → All groups.
For each group in scope:
Open the group → Members.
Export/download membership if available in your portal experience, otherwise capture screenshots.
Record: group name, purpose, and member count.

(5) Build the Role-to-Group / Access mapping table
Create a simple matrix:
Role / Group | What access it grants | How access is granted (direct role vs group membership) | Who has it | Evidence link
Link each row to the relevant screenshot in /evidence/.

(6) Perform the review checks (findings) For each role/group in scope, check and document:
Least privilege: is the role/group too broad for the person’s job?
Stale access: any accounts that shouldn’t still have access (role changes, left team, etc.)?
Duplicates: users with overlapping admin roles or redundant group access.
Naming/ownership: does the group have a clear owner and description?
Break-glass/admin accounts: are they identified and handled intentionally (if your org uses them)?

(7) Document outcomes and actions
For each finding, record one of: Keep / Remove / Investigate.
Write the action owner (who should change it) and a target date.

(8) Package evidence
Save screenshots with consistent names (example):
evidence/roles-global-admin-assignments-2026-05-01.png
evidence/group-it-admins-members-2026-05-01.png
Ensure each Finding links to its evidence file.

Repeat cadence
Note: “Repeat this review monthly/quarterly” and reuse the same scope + checklist, updating the evidence and findings.
