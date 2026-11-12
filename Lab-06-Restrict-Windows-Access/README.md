# Lab 06 — Restrict Access by Operating System

## Objective
Create a Microsoft Entra Conditional Access policy that blocks browser access from the Windows device platform for a dedicated test user.

## Policy configuration captured
- Policy name: `restrict windows Access`
- Included identity: Don Paul (`don@fikayo.onmicrosoft.com`)
- Excluded identity: administrator account
- Target resources: All resources
- Device platform condition: Windows
- Client app condition: Browser
- Grant control: Block access
- Policy state during enforcement test: On

## Test and observed outcome
A browser sign-in was attempted as Don Paul from the Windows 11 workstation. Microsoft sign-in troubleshooting details reported:
- Error code: `53003`
- Application: My Apps
- Device platform: Windows 10
- Device state: Unregistered

The Entra sign-in log showed a failed sign-in. In the Conditional Access tab, the policy `restrict windows Access` appeared with Grant control `Block` and Result `Failure`. Other policies in that event were shown as Disabled or Not applied.

The workstation was Windows 11, but the Microsoft sign-in detail page classified the browser platform as Windows 10. The important observation for this policy is that Entra classified it as the Windows platform selected by the policy.

## Interpretation
The evidence supports that the named Conditional Access policy blocked the test user's browser access. Error `53003` is consistent with a Conditional Access-related denial; the policy-specific Conditional Access tab is the stronger evidence identifying this policy and its Block result.

## Security scope and caution
The policy targets All resources for the selected user and Browser client. It blocks that user's matching Windows browser access broadly. The administrator account is excluded. Keep an administrative session available when managing the policy.

## Evidence

The cleaned screenshot set uses eight unique filenames:

1. `01-test-user-inclusion-don-paul.png`
2. `02-administrator-exclusion.png`
3. `03-windows-platform-condition.png`
4. `04-browser-client-condition.png`
5. `05-block-access-grant-and-enabled-state.png`
6. `06-failed-sign-in-event.png`
7. `07-conditional-access-policy-block-result.png`
8. `08-microsoft-error-53003-windows-platform-details.png`

The evidence index is in `screenshots/README.md`. The PNGs should be uploaded with these exact names from the cleaned evidence ZIP.

## Cleanup / future work
For a reusable lab tenant, either leave the policy On as an intentional demonstration or turn it Off after evidence capture. Do not remove the administrator exclusion while the policy is enabled.
