# Lab 08 — Test Results

## Test scope

This lab verifies that Debbie O can activate an eligible Reports Reader role using the configured authentication context, and that the matching sign-in event records the Conditional Access evaluation.

## Phase D — Activate the eligible role

Debbie activated Reports Reader through **PIM → My roles → Microsoft Entra roles**, using an 8-hour duration and a justification describing the need to review Entra sign-in and audit logs for this lab.

### Observed results

| Validation item | Observed result |
|---|---|
| PIM My roles → Active assignments | Reports Reader shown as Activated |
| PIM Resource audit | `Add member to role completed (PIM activation)` recorded for Debbie O and Reports Reader |
| Audit status | Successful |
| Activation notification | Email confirmed activation and showed the 8-hour start/end time |

## Phase E — Verify Conditional Access evaluation

The matching Conditional Access policy details showed:

| Evaluation field | Observed result |
|---|---|
| Policy | `Require-MFA-Sensitive-Operation` |
| Policy state | Enabled |
| Overall policy result | Success |
| User | Debbie O — Matched |
| Authentication contexts | Matched |
| Grant controls | Satisfied |
| Specific grant control | Require multifactor authentication |
| Session controls | Enforced |

The captured sign-in event demonstrates that Debbie and the authentication context matched the policy, and that the MFA grant requirement was satisfied.

## Prompt behavior and evidence limitation

Debbie did **not** observe a separate, new interactive MFA prompt during the activation attempt.

The sign-in log nevertheless records the matching authentication context, a successful policy result, the MFA grant as **Satisfied**, and session controls as **Enforced**.

Do not describe this evidence as proof that a fresh MFA challenge was visibly displayed. It proves the Conditional Access evaluation and satisfaction of the configured grant control for the captured sign-in event. Microsoft Entra can satisfy an MFA requirement using an authentication state already present in the session, so a new prompt is not guaranteed for every event.

## Evidence index

See [screenshots/README.md](screenshots/README.md) for the ten numbered screenshots and their descriptions.

The evidence index includes:
- Authentication context creation and publication.
- Conditional Access targeting and MFA grant configuration.
- Debbie's eligible Reports Reader assignment.
- PIM activation settings, activation confirmation, and resource audit.
- Sign-in frequency configuration.
- Authentication-context match, policy success, MFA grant satisfaction, and session enforcement.

## Result

**Completed — PIM activation and authentication-context Conditional Access evaluation verified.**

Evidence supports:
1. Authentication context `Sensitive-Operation` (`C1`) was created and published.
2. The Conditional Access policy was enabled, targeted C1, included Debbie, excluded the administrator, and required MFA.
3. PIM Reports Reader activation settings required C1, with an 8-hour maximum and justification.
4. Debbie held an eligible Reports Reader assignment and successfully activated the role.
5. A sign-in event showed Debbie and the authentication context matched, the policy result was Success, the MFA grant control was Satisfied, and session controls were Enforced.

## Cleanup and safety

- Keep the administrator excluded from the Conditional Access policy.
- Leave the policy On only if this behavior is intended for the test user and context. Otherwise turn it Off after evidence capture.
- Decide whether to leave Debbie's Reports Reader assignment eligible after testing.
- Keep the lab tenant non-production.
- Never publish passwords, temporary codes, authentication tokens, client secrets, certificates, private keys, or recovery codes.
