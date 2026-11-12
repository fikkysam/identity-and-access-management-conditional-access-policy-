# Lab 02 — Protect Azure Management: Screenshot Evidence

This folder documents the `Protect-Azure-Management` Microsoft Entra Conditional Access policy.

## Evidence index

| # | Screenshot | Evidence |
|---|---|---|
| 01 | [01-excluded-administrator.png](01-excluded-administrator.png) | Administrator account excluded from the policy |
| 02 | [02-included-test-user.png](02-included-test-user.png) | Debbie O selected as the included test user |
| 03 | [03-target-resource-azure-resource-manager.png](03-target-resource-azure-resource-manager.png) | Azure Resource Manager selected as the target resource |
| 04 | [04-grant-control-require-mfa.png](04-grant-control-require-mfa.png) | Grant access with Require multifactor authentication |
| 05 | [05-policy-configuration-report-only.png](05-policy-configuration-report-only.png) | Original policy configuration in Report-only mode |
| 06 | [06-policy-details-summary.png](06-policy-details-summary.png) | Original policy details and Report-only state |
| 07 | [07-azure-portal-sign-in-event.png](07-azure-portal-sign-in-event.png) | Azure Portal sign-in event associated with Azure Resource Manager |
| 08 | [08-report-only-policy-evaluation.png](08-report-only-policy-evaluation.png) | Original Report-only policy evaluation |
| 09 | [09-enforced-mfa-conditional-access-success.png](09-enforced-mfa-conditional-access-success.png) | Enforced policy evaluation: `Protect-Azure-Management`, MFA grant control, result Success |
| 10 | [10-mfa-authentication-details.png](10-mfa-authentication-details.png) | Authentication details: Previously satisfied, Succeeded Yes, MFA requirement satisfied |

## Policy configuration

- **Policy name:** `Protect-Azure-Management`
- **Included test user:** Debbie O (`debbie@fikayo.onmicrosoft.com`)
- **Excluded identity:** Administrator account
- **Target resource:** Azure Resource Manager
- **Grant control:** Grant access; Require multifactor authentication
- **Policy state during enforcement validation:** On
- **Conditions:** No additional conditions selected

## Enforcement validation

The additional sign-in evidence records:

- Application: Azure Portal
- Resource: Azure Resource Manager
- Sign-in status: Success
- `Protect-Azure-Management` grant control: MFA
- `Protect-Azure-Management` result: **Success**
- Authentication details: **Previously satisfied**, **Succeeded: Yes**, with the MFA requirement satisfied

**Interpretation:** The policy evaluation succeeded and the MFA requirement was satisfied. The authentication details say **Previously satisfied**, so the screenshots do not establish that a fresh MFA prompt appeared during this specific sign-in. Use the precise wording “MFA requirement satisfied through Conditional Access.”

## Privacy handling

Names, email addresses, tenant/account header details, request IDs, and policy configuration remain visible. IP address information should be blurred in any sign-in log screenshot uploaded to this repository.
