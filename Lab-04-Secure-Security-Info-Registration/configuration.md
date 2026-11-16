# Lab 04 — Configuration

## Prerequisites

- Microsoft Entra Conditional Access capability.
- A dedicated test identity.
- A separate administrator account.
- A known and usable recovery/authentication method for the test identity.
- Conditional Access support for targeting the Register security information user action.

## Final policy details

| Setting | Value |
|---|---|
| Policy name | `Require MFA for Security Info Registration` |
| Users — Include | Don Paul (`don@fikayo.onmicrosoft.com`) |
| Users — Exclude | Administrator account |
| Target resources | User actions |
| Selected user action | Register security information |
| Grant | Grant access |
| Grant control | Require multifactor authentication |
| Policy state | On |

## Configuration procedure

1. Sign in to the Microsoft Entra admin center using the separate administrator account.
2. Navigate to **Conditional Access → Policies**.
3. Open or create the policy `Require MFA for Security Info Registration`.
4. Under **Users → Include**, select the dedicated test user, Don Paul.
5. Under **Users → Exclude**, select the administrator account.
6. Under **Target resources**, select **User actions**.
7. Select **Register security information**.
8. Open **Access controls → Grant**.
9. Select **Grant access** and **Require multifactor authentication**.
10. Save the policy and confirm that its state is **On**.

## Configuration validation

The screenshot evidence index records:
- Policy overview and enabled state.
- Test-user inclusion.
- Register security information user action.
- Administrator exclusion.
- Grant access with Require multifactor authentication selected.

See [screenshots/README.md](screenshots/README.md) for the ten-item evidence index.

## Safety controls

- Keep the administrator and emergency access identities excluded.
- Confirm the test identity has a usable authentication method or approved bootstrap/recovery method.
- Keep the policy scoped to the intended test user and user action.
- Never publish passwords, temporary codes, authentication tokens, or recovery codes.
