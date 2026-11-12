# Lab 02 — Protect Azure Management: Evidence Package

This package contains ten screenshots documenting the Microsoft Entra Conditional Access policy `Protect-Azure-Management` and its validation.

## Evidence index

| # | Screenshot | Evidence |
|---|---|---|
| 01 | `01-excluded-administrator.png` | Administrator account excluded from the policy |
| 02 | `02-included-test-user.png` | Debbie O selected as the included test user |
| 03 | `03-target-resource-azure-resource-manager.png` | Azure Resource Manager selected as the target resource |
| 04 | `04-grant-control-require-mfa.png` | Grant access with Require multifactor authentication |
| 05 | `05-policy-configuration-report-only.png` | Original policy configuration in Report-only mode |
| 06 | `06-policy-details-summary.png` | Original policy details and Report-only state |
| 07 | `07-azure-portal-sign-in-event.png` | Azure Portal sign-in event associated with Azure Resource Manager |
| 08 | `08-report-only-policy-evaluation.png` | Original Report-only policy evaluation |
| 09 | `09-enforced-mfa-conditional-access-success.png` | Enforced policy evaluation: `Protect-Azure-Management`, MFA grant control, result Success |
| 10 | `10-mfa-authentication-details.png` | Authentication details: Previously satisfied, Succeeded Yes, MFA requirement satisfied |

## Policy configuration

- **Policy name:** `Protect-Azure-Management`
- **Included test user:** Debbie O (`debbie@fikayo.onmicrosoft.com`)
- **Excluded identity:** Administrator account
- **Target resource:** Azure Resource Manager
- **Grant control:** Grant access; Require multifactor authentication
- **Policy state during enforcement validation:** On
- **Conditions:** No additional conditions selected

## Validation interpretation

The additional sign-in evidence records an Azure Portal sign-in to Azure Resource Manager. The `Protect-Azure-Management` Conditional Access policy shows **Success**, with **MFA** as its grant control. Authentication details show **Previously satisfied**, **Succeeded: Yes**, and an MFA requirement satisfied result.

This supports the statement **“MFA requirement satisfied through Conditional Access.”** The authentication details say **Previously satisfied**, so the evidence does not establish that a fresh MFA prompt appeared during this particular sign-in.

## Privacy

IP address information is redacted in the original sign-in event evidence. Names, email addresses, tenant/account context, request IDs, and policy configuration are retained for portfolio attribution and technical context.
