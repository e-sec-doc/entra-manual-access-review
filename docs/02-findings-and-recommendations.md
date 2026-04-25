Two users were found to be mismatched to the role-to-group matrix.

| User | Current group | Expected group | Risk / Why it matters | Recommendation | Status | Evidence |
|---|---|---|---|---|---|---|
| `test.user3` | `IT-Admins` | `Contractors` | Excess privilege: contractor has access intended for IT admins. Compromise could impact admin-level resources. | Remove from `IT-Admins`; add to `Contractors` | Pending approval | `evidence/it-admins.png` |
| `test.user7` | `HR-App-Users` | `IT-Admins` | Incorrect access assignment: user may lack required IT access and has unnecessary HR app access. | Remove from `HR-App-Users`; add to `IT-Admins` | Pending approval | `evidence/hr-app-users.png` |
