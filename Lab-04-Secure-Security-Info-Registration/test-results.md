# Lab 04 — Test Results

## Test objective

Validate that the Conditional Access policy protecting the **Register security information** user action is configured to require MFA, and review the captured authentication and sign-in evidence.

## Observed results

| Test / evidence | Observed result |
|---|---|
| Policy enabled | Confirmed |
| Test-user inclusion | Confirmed |
| Administrator exclusion | Confirmed |
| Target user action | Register security information |
| Grant control | Require multifactor authentication |
| Authenticator challenge | Microsoft Authenticator number-matching prompt captured |
| Security information registration | Microsoft Authenticator shown as a registered method |
| Conditional Access evaluation | Named policy shown with MFA grant control and Success |
| Sign-in events view | Successful sign-in and Conditional Access status captured |

## Evidence interpretation

The screenshot set contains a visible Microsoft Authenticator number-matching challenge, a security information page showing Microsoft Authenticator as a registered method, and a Conditional Access evaluation showing the named policy, MFA grant control, and **Success**.

These items support completion of the policy configuration and the authentication/registration validation exercise.

**Correlation limitation:** The sign-in summary screenshot does not, by itself, prove every detail of the authentication sequence for the exact security-information registration transaction. To make that narrower claim, inspect the individual sign-in event's authentication details and correlate its timestamp, user, and activity with the registration attempt. Do not infer that correlation solely from a general successful sign-in summary.

## Evidence index

See [screenshots/README.md](screenshots/README.md) for the ten numbered screenshots and their descriptions.

## Completion checklist

- [x] Dedicated test user included.
- [x] Administrator account excluded.
- [x] Register security information user action selected.
- [x] Grant access configured.
- [x] Require multifactor authentication selected.
- [x] Policy enabled.
- [x] Microsoft Authenticator number-matching prompt captured.
- [x] Microsoft Authenticator registration shown.
- [x] Successful Conditional Access evaluation captured.
- [x] Sign-in events and Conditional Access status evidence captured.

## Result

**Lab 04 completed — policy configuration and supporting authentication/registration evidence captured.**

The evidence supports the enabled MFA policy, the intended user-action target, the Authenticator number-matching challenge, registration of the Authenticator method, and a successful Conditional Access evaluation. The event-to-transaction correlation limitation above is retained for technical accuracy.
