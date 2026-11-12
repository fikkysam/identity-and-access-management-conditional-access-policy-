# Lab 04 — Secure Security Information Registration

## Objective

Require multifactor authentication (MFA) when a user performs the **Register security information** user action.

## Policy configuration

- **Policy name:** Require MFA for Security Info Registration
- **Target:** User action — Register security information
- **Users:** Specific test user included; administrator account excluded
- **Grant:** Grant access — Require multifactor authentication
- **Policy state:** On

## Screenshot evidence

Upload the ten PNG files listed below into this folder. The filenames are numbered in review order.

| # | Filename | Evidence |
|---:|---|---|
| 01 | `01-policy-overview-and-enabled-state.png` | Conditional Access policy overview and enabled state |
| 02 | `02-policy-user-inclusion.png` | Test user selected in the policy inclusion scope |
| 03 | `03-target-action-register-security-information.png` | Policy targets the Register security information user action |
| 04 | `04-policy-administrator-exclusion.png` | Administrator account exclusion |
| 05 | `05-grant-control-require-mfa.png` | Grant access with Require multifactor authentication selected |
| 06 | `06-microsoft-authenticator-number-matching-prompt.png` | Microsoft Authenticator approval request with number matching |
| 07 | `07-security-info-authenticator-method-registered.png` | Security info page showing Microsoft Authenticator as a registered method |
| 08 | `08-conditional-access-mfa-success.png` | Conditional Access details showing this policy, MFA grant control, and Success |
| 09 | `09-security-info-registration-policy-enabled.png` | Registration action configuration and policy On state |
| 10 | `10-sign-in-events-conditional-access-validation.png` | Sign-in events view with successful sign-in and Conditional Access status |

## Validation notes

The evidence set includes the policy configuration, an Authenticator number-matching prompt, a registered Authenticator method, and a Conditional Access evaluation showing **MFA** with a **Success** result for the named policy.

The screenshots establish the policy configuration and successful Conditional Access evaluation. The sign-in summary alone does not establish every detail of the authentication sequence for the specific security-information registration transaction; consult the individual sign-in's authentication details when documenting that precise correlation.
