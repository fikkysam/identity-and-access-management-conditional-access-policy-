# Lab 02 — Protect Azure Management: Screenshot Evidence

## Upload status

The original screenshots have been removed. The replacement IP-only redacted screenshots have **not yet been uploaded**. At present, this folder contains this index file only.

Once the replacement images are uploaded, use the exact filenames below so the evidence index and Lab 02 documentation remain consistent.

## Planned evidence index

| # | Filename | Evidence |
|---|---|---|
| 01 | `01-excluded-administrator.png` | Administrator account excluded from the policy |
| 02 | `02-included-test-user.png` | Debbie O selected as the included test user |
| 03 | `03-target-resource-azure-resource-manager.png` | Azure Resource Manager selected as the target resource |
| 04 | `04-grant-control-require-mfa.png` | Grant access with Require multifactor authentication |
| 05 | `05-policy-configuration-report-only.png` | Policy configuration and Report-only enablement |
| 06 | `06-policy-details-summary.png` | Policy details, Report-only state, and MFA requirement |
| 07 | `07-azure-portal-sign-in-event.png` | Azure Portal sign-in event associated with Azure Resource Manager |
| 08 | `08-report-only-policy-evaluation.png` | Conditional Access Report-only evaluation |

## Policy configuration

- **Policy name:** `Protect-Azure-Management`
- **Included test user:** Debbie O
- **Excluded identity:** One administrator account
- **Target resource:** Azure Resource Manager
- **Grant control:** Grant access; Require multifactor authentication
- **Policy state:** Report-only
- **Conditions:** No conditions selected

## Test result and interpretation

The sign-in evidence captured for this lab showed an Azure Portal sign-in with Azure Resource Manager as the resource. The Report-only evaluation listed `Protect-Azure-Management` and the MFA grant control. The displayed result began `Report-only: User action required`; the remaining text was truncated in the original screenshot.

Because the policy is in **Report-only** mode, it is evaluated for impact but is not enforced. This evidence documents policy configuration and Report-only evaluation; it does not demonstrate an enforced MFA challenge.

## Privacy handling

The replacement evidence is intended to retain names, email addresses, tenant/account header details, request IDs, and policy configuration. Only IP address information should be blurred, as requested.
