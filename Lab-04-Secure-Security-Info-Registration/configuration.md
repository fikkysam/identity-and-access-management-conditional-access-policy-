# Lab 04 — Configuration

## Prerequisites

- Microsoft Entra Conditional Access capability.
- A dedicated test identity.
- A separate administrator account.
- A known and usable recovery/authentication method for the test identity.
- Conditional Access support for targeting the Register security information user action.

## Policy details captured so far

| Setting | Value |
|---|---|
| Policy name | `Require MFA for Security Info Registration` |
| Users — Include | Users and groups → don paul |
| Users — Exclude | Users and groups → Oluwafikayo Oyedokun (administrator) |
| Target resources | User actions |
| Selected user action | Register security information |
| Grant controls | Not configured in the captured creation screen |
| Enable policy | Report-only |

## Configuration procedure

1. Sign in to the Microsoft Entra admin center using the separate administrator account.
2. Navigate to **Conditional Access → Policies → New policy**.
3. Enter the name `Require MFA for Security Info Registration`.
4. Under **Users → Include**, select the dedicated test user, shown in the captured configuration as **don paul**.
5. Under **Users → Exclude**, select the administrator account. The captured configuration excludes **Oluwafikayo Oyedokun**.
6. Under **Target resources**, select **User actions**.
7. Select **Register security information** and confirm that one user action is included.
8. Open **Access controls → Grant**.
9. Select **Grant access** and require MFA or an appropriate authentication strength supported by the tenant.
10. Save the policy in **Report-only**.
11. Review the completed policy before testing.

## Configuration still outstanding

The latest captured creation screen shows **0 controls selected** under Grant. Do not treat the policy as complete until the MFA/authentication-strength grant requirement has been selected and the policy has been created.

## Safety controls

- Keep the administrator and emergency access accounts excluded.
- Confirm the test identity can complete the required authentication challenge.
- Establish a secure bootstrap/recovery method before testing security information registration.
- Keep the policy in Report-only during initial validation.
