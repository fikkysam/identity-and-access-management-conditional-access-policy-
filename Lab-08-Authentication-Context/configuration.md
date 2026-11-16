# Lab 08 — Configuration

## Prerequisites

- Microsoft Entra ID P2 in the lab tenant.
- A separate administrator account for configuration.
- Dedicated test user: Debbie O (`debbie@fikayo.onmicrosoft.com`).
- Privileged Identity Management (PIM) available for Microsoft Entra roles.
- Reports Reader role available for the eligibility and activation exercise.

## Environment and identities

| Item | Value |
|---|---|
| Tenant | `fikayo` |
| Test user | Debbie O (`debbie@fikayo.onmicrosoft.com`) |
| Administrator | Separate administrator account, excluded from the Conditional Access policy |
| Licensing recorded for this lab | Microsoft Entra ID P2 |
| PIM role | Reports Reader |

## Phase A — Create the authentication context

Navigate to **Microsoft Entra ID → Conditional Access → Authentication contexts** and create the context.

| Setting | Configured value |
|---|---|
| Name | `Sensitive-Operation` |
| Description | Require stronger authentication before a user performs a sensitive operation in the lab application. |
| Publish to apps | Enabled |
| Context ID | `C1` |

## Phase B — Configure the Conditional Access policy

Create the policy `Require-MFA-Sensitive-Operation`.

| Setting | Configured value |
|---|---|
| Users included | Debbie O (`debbie@fikayo.onmicrosoft.com`) |
| Users excluded | Administrator account |
| Target | Authentication context |
| Selected context | `Sensitive-Operation` (`C1`) |
| Grant | Grant access |
| Grant control | Require multifactor authentication |
| Session control | Sign-in frequency — Every time |
| Policy state | On |

The policy targets authentication context C1 rather than all resources. A sign-in to an unrelated resource can correctly show **Not applied** when that event does not request or match this authentication context.

## Phase C — Configure PIM for Reports Reader

Navigate to **Privileged Identity Management → Microsoft Entra roles → Reports Reader → Role settings**.

| Setting | Configured value |
|---|---|
| Maximum activation duration | 8 hours |
| On activation, require | Microsoft Entra Conditional Access authentication context |
| Selected context | `Sensitive-Operation` (`C1`) |
| Require justification | Enabled |
| Require ticket information | Disabled |

Debbie O was assigned **eligible** membership in Reports Reader. Eligible membership means the role is not permanently active; Debbie must activate it when the role is needed.

> **Scope caution:** PIM role settings apply to the role across the tenant, not only to Debbie's assignment. Review existing assignments before changing settings on a shared role.

## Configuration evidence

See [screenshots/README.md](screenshots/README.md) for the numbered evidence index covering the authentication context, Conditional Access policy, PIM assignment and role settings, and sign-in evaluation.

## Operational notes

- Keep the administrator excluded from the Conditional Access policy.
- Review the policy state before using this configuration outside the non-production lab.
- Review existing role assignments before changing shared PIM role settings.
- Never publish passwords, temporary codes, authentication tokens, client secrets, certificates, private keys, or recovery codes.
