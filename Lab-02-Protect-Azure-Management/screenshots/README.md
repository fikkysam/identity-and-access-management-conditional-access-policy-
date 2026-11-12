# Lab 02 — Protect Azure Management

## Evidence screenshots

This folder contains the selected screenshots documenting the `Protect-Azure-Management` Microsoft Entra Conditional Access policy.

| # | Screenshot | Evidence |
|---|---|---|
| 01 | `01-excluded-administrator.png` | Administrator account excluded from the policy |
| 02 | `02-included-test-user.png` | Debbie O selected as the included test user |
| 03 | `03-target-resource-azure-resource-manager.png` | Azure Resource Manager selected as the target resource |
| 04 | `04-grant-control-require-mfa.png` | Grant access with Require multifactor authentication |
| 05 | `05-policy-configuration-report-only.png` | Policy configuration and Report-only enablement |
| 06 | `06-policy-details-summary.png` | Policy details, including Report-only state and MFA requirement |
| 07 | `07-azure-portal-sign-in-event.png` | Azure Portal sign-in event associated with Azure Resource Manager |
| 08 | `08-report-only-policy-evaluation.png` | Conditional Access Report-only evaluation for the policy |

## Policy configuration

- **Policy name:** `Protect-Azure-Management`
- **Included user:** Debbie O
- **Excluded identity:** One administrator account
- **Target resource:** Azure Resource Manager
- **Grant control:** Grant access; Require multifactor authentication
- **Policy state:** Report-only
- **Conditions:** No conditions selected

## Test result and interpretation

The sign-in evidence shows an Azure Portal sign-in with Azure Resource Manager as the resource. The Report-only evaluation lists `Protect-Azure-Management` and the MFA grant control. Its result is displayed as `Report-only: User action required` (the screenshot truncates the end of the text).

Because the policy is in **Report-only** mode, it is evaluated for impact but is not enforced. This lab therefore documents policy configuration and Report-only evaluation; it does not demonstrate an enforced MFA challenge.

## Evidence handling

Review screenshots before publishing them publicly. Mask tenant identifiers, user principal names, IP addresses, request IDs, or other identifying details if they are not intended for public disclosure.
