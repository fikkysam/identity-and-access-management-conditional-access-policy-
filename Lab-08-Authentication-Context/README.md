# Lab 08 — Authentication Context with PIM

## Objective

Use a Microsoft Entra authentication context and Conditional Access policy to add an MFA requirement to Privileged Identity Management (PIM) activation for an eligible Microsoft Entra role assignment.

This implementation uses PIM directly. A custom Node.js application is **not** part of this lab.

## Lab environment

- Tenant: `fikayo`
- Test user: Debbie O (`debbie@fikayo.onmicrosoft.com`)
- Administrator: separate administrator account, excluded from the Conditional Access policy
- Microsoft Entra licensing recorded for this lab: Entra ID P2
- PIM role: Reports Reader

## Implementation summary

1. Created and published the `Sensitive-Operation` authentication context (ID `C1`).
2. Enabled the `Require-MFA-Sensitive-Operation` Conditional Access policy for Debbie, excluding the administrator, targeting context C1, and requiring MFA.
3. Configured Reports Reader PIM activation to require context C1, with an 8-hour maximum activation duration and justification.
4. Assigned Debbie eligible Reports Reader membership and verified a successful activation.
5. Reviewed the matching sign-in event and confirmed the authentication context matched, the policy result was Success, the MFA grant was Satisfied, and session controls were Enforced.

## Documentation

| Document | Purpose |
|---|---|
| [configuration.md](configuration.md) | Authentication context, Conditional Access policy, and PIM configuration |
| [test-results.md](test-results.md) | PIM activation, sign-in evaluation, observed results, and evidence interpretation |
| [screenshots/README.md](screenshots/README.md) | Numbered screenshot evidence index |

## Result

**Completed — PIM activation and authentication-context Conditional Access evaluation verified.**

### Important evidence limitation

Debbie did not observe a separate, new interactive MFA prompt during the activation attempt. The captured sign-in event proves that the MFA grant requirement was satisfied during Conditional Access evaluation; it does not prove that a fresh interactive challenge was visibly displayed. See [test-results.md](test-results.md) for the full explanation.

## Safety and operational notes

- Keep the administrator excluded from the Conditional Access policy.
- PIM role settings apply to the role across the tenant, not only to Debbie's assignment. Review existing assignments before changing settings on a shared role.
- Leave the policy On only if this behavior is intended for the test user and context. Otherwise turn it Off after evidence capture.
- Decide whether to leave Debbie's Reports Reader assignment eligible after testing.
- Keep the lab tenant non-production.
- Never publish passwords, temporary codes, authentication tokens, client secrets, certificates, private keys, or recovery codes.
