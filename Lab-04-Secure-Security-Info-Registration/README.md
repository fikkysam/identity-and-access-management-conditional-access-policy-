# Lab 04 — Protect Security Information Registration

## Objective

Protect the user action used to register or manage authentication methods by requiring multifactor authentication (MFA).

## Security context

Security information registration changes the authentication methods available to an identity. Protecting this user action helps reduce the risk that an attacker who has obtained a session can register an authentication method they control.

## Lab environment

- Microsoft Entra ID non-production tenant
- Separate administrator account used to configure the policy
- Dedicated test identity: Don Paul (`don@fikayo.onmicrosoft.com`)
- Administrator identity excluded from the policy

## Final policy configuration

| Setting | Observed configuration |
|---|---|
| Policy name | `Require MFA for Security Info Registration` |
| Included user | Don Paul |
| Excluded user | Administrator account |
| Target resource type | User actions |
| User action | Register security information |
| Grant control | Grant access — Require multifactor authentication |
| Policy state | On |

## Implementation and validation

The policy was configured to target the **Register security information** user action and require MFA. The final evidence set records:

1. The policy overview and enabled state.
2. The dedicated test user inclusion and administrator exclusion.
3. The Register security information user action selection.
4. The Require multifactor authentication grant control.
5. A Microsoft Authenticator number-matching prompt.
6. Microsoft Authenticator shown as a registered security information method.
7. A Conditional Access sign-in evaluation showing the named policy, MFA grant control, and Success.
8. A sign-in events view showing a successful sign-in and Conditional Access status.

## Result

**Completed — Conditional Access MFA policy configuration and supporting authentication/registration evidence captured.**

The evidence demonstrates that the policy is enabled, targets the intended user action, requires MFA, and has a successful Conditional Access evaluation. The evidence set also includes a visible Microsoft Authenticator number-matching challenge and the registered Authenticator method.

**Evidence interpretation:** The screenshots establish the policy configuration and successful Conditional Access evaluation. The sign-in summary alone does not establish every detail of the authentication sequence for the specific security-information registration transaction. For a strict event-to-transaction correlation, inspect the individual sign-in's authentication details.

## Safety notes

- Keep the administrator and emergency access identities excluded.
- Maintain a usable recovery/authentication method for the test identity.
- Keep the policy scoped to the intended test users and user action.
- Do not publish passwords, temporary codes, authentication tokens, or recovery codes.

See [configuration.md](configuration.md), [test-results.md](test-results.md), and [screenshots/README.md](screenshots/README.md) for the detailed configuration, validation record, and evidence index.
