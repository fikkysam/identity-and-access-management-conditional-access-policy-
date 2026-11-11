# Lab 02 — Test Results

## Test execution

The dedicated test account signed in to the Azure portal:

- Test identity: `debbie@fikayo.onmicrosoft.com`
- Application: Azure Portal
- Target resource: Azure Resource Manager
- Sign-in status: Success

A fresh interactive sign-in event was generated after the policy was created. The event was opened in **Microsoft Entra admin center → Monitoring & health → Sign-in logs → User sign-ins (interactive)**.

## Report-only evaluation

The Report-only tab for the matching Azure Portal / Azure Resource Manager event displayed the policy:

| Evaluation item | Observed result |
|---|---|
| Policy name | `Protect-Azure-Management` |
| Grant control | MFA |
| Report-only result | `Report-only: User action required` (visible text was truncated in the screenshot) |

Other Report-only policies were also listed in the event. This lab's result was taken from the row named `Protect-Azure-Management`, not from unrelated policies.

## Interpretation

The policy appeared in the Report-only evaluation for the fresh sign-in event. This confirms that the event matched the policy scope sufficiently for Entra to evaluate its MFA grant control.

The displayed **User action required** result indicates that user interaction would be needed to satisfy the MFA requirement. The sign-in itself succeeded because the policy was configured in Report-only mode; Report-only evaluates policy impact but does not enforce the grant control.

Do not interpret the successful Azure portal sign-in as proof that this policy enforced MFA. No enforcement test was performed.

## Result

**Lab 02 configuration and policy matching: passed.**

Evidence confirms:
- The test user was included in the policy.
- One administrator identity was excluded.
- Azure Resource Manager was selected as the target resource.
- Require multifactor authentication was configured as the grant control.
- The policy remained Report-only.
- A fresh Azure Portal sign-in event for Azure Resource Manager listed the policy in its Report-only evaluation.

**Enforced MFA: not tested.** The policy remains Report-only.

## Evidence checklist

- [x] Policy details showing Report-only state.
- [x] Policy details showing one included user and one excluded identity.
- [x] Policy details showing Require multifactor authentication.
- [x] Policy creation view showing Azure Resource Manager selected.
- [x] Fresh interactive sign-in event showing Debbie, Azure Portal, Azure Resource Manager, and Success.
- [x] Report-only tab showing `Protect-Azure-Management`, MFA grant control, and User action required result.

## Limitations

- The Report-only result text was partially truncated in the captured screenshot. The visible portion reads `Report-only: User acti...`; the detailed full result should be captured if the row can be opened or the table column widened.
- The test validates policy matching and Report-only evaluation only. It does not prove that an enforced MFA prompt would appear.
- The lab guide's target label was Microsoft Azure Management; the tenant resource picker exposed Azure Resource Manager, which was selected and then confirmed by the resource field in the sign-in event.
