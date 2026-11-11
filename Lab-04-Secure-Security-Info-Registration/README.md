# Lab 04 — Protect Security Information Registration

## Objective

Protect the user action used to register or manage authentication methods by requiring multifactor authentication or an appropriate authentication strength.

## Security context

Security information registration changes the authentication methods available to an identity. Protecting this user action helps reduce the risk that an attacker who has obtained a session can register an authentication method they control.

## Lab environment

- Microsoft Entra ID non-production tenant
- Separate administrator account used to configure the policy
- Dedicated test identity: don paul
- Administrator identity excluded from the policy

## Current policy configuration

| Setting | Observed configuration |
|---|---|
| Policy name | `Require MFA for Security Info Registration` |
| Included user | don paul |
| Excluded user | Oluwafikayo Oyedokun (administrator) |
| Target resource type | User actions |
| User action | Register security information (1 user action included) |
| Grant controls | None selected yet |
| Policy state | Report-only (creation screen) |

## Current status

<badge>In progress</badge>

The screenshots show the policy scope and the **Register security information** user action selected. However, the Grant section still shows **0 controls selected**, and the policy is on the creation screen. The policy has therefore not yet been completed or validated.

## Remaining work

1. Open **Access controls → Grant**.
2. Select **Grant access**.
3. Require multifactor authentication or an appropriate authentication strength supported by the tenant.
4. Save the policy in **Report-only**.
5. Use the dedicated test identity to access the security information registration page in a controlled session.
6. Review the matching sign-in event and the Conditional Access evaluation.
7. Record the observed result and capture the final policy and sign-in evidence.

## Safety notes

- Keep the administrator and emergency access identities excluded.
- Ensure the test identity has a usable authentication method or approved bootstrap method before testing registration.
- Do not enforce the policy until the test user can satisfy the requirement and a recovery route is confirmed.
- Do not claim the lab passed until the grant control is configured and the matching evaluation is captured.

See [configuration.md](configuration.md) and [test-results.md](test-results.md) for the current record.
