# Findings and recommendations

## Status
All remediation actions in this lab are **recommendations only** and are **pending approval**.

## Summary
Two users were found to be mismatched to the role-to-group access matrix.

---

## Finding 1 — `test.user3`
- **Role/Division:** Electrician (Contractor)
- **Current group:** `IT-Admins`
- **Expected group:** `Contractors`

### Risk / why it matters
This is **excess privilege**. A contractor in an admin group may gain access to IT-admin resources that are not required for the role. If the account is compromised, the impact could be significantly higher.

### Recommendation (pending approval)
- Remove `test.user3` from `IT-Admins`
- Add `test.user3` to `Contractors`

### Evidence
![it-admins evidence](../evidence/it-admins.png)

---

## Finding 2 — `test.user7`
- **Role/Division:** Equipment Technician (IT)
- **Current group:** `HR-App-Users`
- **Expected group:** `IT-Admins`

### Risk / why it matters
This is an **incorrect access assignment**. The user may be missing required IT access while also holding unnecessary HR application access.

### Recommendation (pending approval)
- Remove `test.user7` from `HR-App-Users`
- Add `test.user7` to `IT-Admins`

### Evidence
![hr-app-users evidence](../evidence/hr-app-users.png)
