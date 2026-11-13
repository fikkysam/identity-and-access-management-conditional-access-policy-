# Lab 08 — Authentication Context with PIM

## Objective

Use a Microsoft Entra authentication context and Conditional Access policy to add an MFA requirement to Privileged Identity Management (PIM) activation for an eligible Microsoft Entra role assignment.

This implementation uses PIM directly. A custom Node.js application is **not** part of this lab.

## Environment and identities

- Tenant: `fikayo`
- Test user: Debbie O (`debbie@fikayo.onmicrosoft.com`)
- Administrator: separate administrator account, excluded from the Conditional Access policy
- Microsoft Entra licensing: Entra ID P2 (as confirmed for this lab tenant)
- PIM role used: Reports Reader

## Phase A — Create the authentication context

Created in **Entra ID → Conditional Access → Authentication contexts**:

| Setting | Value |
|---|---|
| Name | `Sensitive-Operation` |
| Description | Require stronger authentication before a user performs a sensitive operation in the lab application. |
| Publish to apps | Enabled |
| Context ID | `C1` |

## Phase B — Configure the Conditional Access policy

Policy: `Require-MFA-Sensitive-Operation`

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

The policy targets the authentication context, not all resources. A sign-in to an unrelated resource can correctly show **Not applied** when that event does not request or match the authentication context.

## Phase C — Configure PIM for Reports Reader

In **Privileged Identity Management → Microsoft Entra roles → Reports Reader → Role settings**, activation settings were configured:

| Setting | Value |
|---|---|
| Maximum activation duration | 8 hours |
| On activation, require | Microsoft Entra Conditional Access authentication context |
| Selected context | `Sensitive-Operation` (`C1`) |
| Require justification | Enabled |
| Require ticket information | Disabled |

Debbie O was assigned **eligible** membership in Reports Reader. Eligible means the role is not permanently active; Debbie must activate it when the role is needed.

**Scope caution:** PIM role settings apply to the role across the tenant, not only to Debbie's assignment. Review existing assignments before changing settings on a shared role.

## Phase D — Activate the eligible role

Debbie activated Reports Reader through **PIM → My roles → Microsoft Entra roles** using an 8-hour duration and a justification describing the need to review Entra sign-in and audit logs for this lab.

Observed evidence:
- PIM **My roles → Active assignments** showed Reports Reader as Activated.
- PIM **Resource audit** showed `Add member to role completed (PIM activation)` for Debbie O and Reports Reader, with successful status.
- The activation notification email confirmed Debbie activated Reports Reader and showed the 8-hour start/end time.

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

The sign-in event demonstrates that Debbie and the authentication context matched the policy and that the MFA grant requirement was satisfied.

### Prompt behavior and evidence limitation

Debbie did **not** observe a separate, new interactive MFA prompt during the activation attempt. The sign-in log nevertheless records the matching authentication context, a successful policy result, the MFA grant as **Satisfied**, and session controls as **Enforced**.

Do not describe this evidence as proof that a fresh MFA challenge was visibly displayed. It proves the Conditional Access evaluation and satisfaction of the configured grant control for the captured sign-in event. Microsoft Entra can satisfy an MFA requirement using an authentication state already present in the session, so a new prompt is not guaranteed for every event.

## Outcome

**Completed — PIM activation and authentication-context Conditional Access evaluation verified.**

Evidence supports:
1. Authentication context `Sensitive-Operation` (`C1`) was created and published.
2. The Conditional Access policy was enabled, targeted C1, included Debbie, excluded the administrator, and required MFA.
3. PIM Reports Reader activation settings required C1, with an 8-hour maximum and justification.
4. Debbie held an eligible Reports Reader assignment and successfully activated the role.
5. A sign-in event showed Debbie and the authentication context matched, the policy result was Success, the MFA grant control was Satisfied, and session controls were Enforced.

## Evidence

See `screenshots/README.md` for the numbered evidence index. Screenshots document the context, Conditional Access policy, PIM role settings and assignment, successful activation and audit history, sign-in frequency configuration, and the policy-specific sign-in evaluation.

Never publish passwords, temporary codes, authentication tokens, client secrets, certificates, private keys, or recovery codes.

## Cleanup and operational notes

- Keep the administrator excluded from the Conditional Access policy.
- Leave the policy On only if this behavior is intended for the test user and context. Otherwise turn it Off after evidence capture.
- Decide whether to leave Debbie's Reports Reader assignment eligible after testing.
- Keep the lab tenant non-production.
