# Manual access review procedure (no Entra ID P2)

## Objective
Validate that user group membership aligns with the approved **Role-to-Group Access Matrix**.

## Inputs (source of truth)
- Role-to-Group Access Matrix (in `README.md`)
- User-to-Role Mapping (in `README.md`)

## Tools
- Microsoft Entra admin center (Groups + Users)
- Screenshots saved under `/evidence`

## Procedure
1. Confirm the approved Role-to-Group Access Matrix (expected groups per role).
2. For each user, check current Entra group membership.
3. Compare **current group** vs **expected group** based on the user’s role.
4. Record results (Match / Mismatch) and notes.
5. For each mismatch:
   - Write a short risk statement (why it matters).
   - Write a clear recommendation (remove/add group).
6. Capture evidence screenshots and save them in `/evidence`.
7. Mark remediation as **Pending approval** (no changes implemented in this lab).

## Output
- Findings summary + evidence screenshots that support each mismatch.

