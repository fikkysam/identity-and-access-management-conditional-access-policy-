# Lab 07 — Test Results

## Test objective

Verify that the Conditional Access device filter matches a device not identified as Company-owned and blocks the selected user's browser access.

## Test procedure

1. Confirm `Block-NonCompany-Devices` is On.
2. Confirm Don Paul is included and the administrator account is excluded.
3. Confirm the filter mode is **Include filtered devices in policy**.
4. From the Windows workstation, attempt browser access to My Apps as Don Paul.
5. Open the corresponding sign-in event and inspect the device details and **Conditional Access** tab.
6. Confirm the Lab 06 policy is not responsible for the result.

## Observed results

| Field | Observed value |
|---|---|
| Test date | November 12, 2026 |
| Test identity | Don Paul (`don@fikayo.onmicrosoft.com`) |
| Application | My Apps |
| Device platform reported by Entra | Windows 10 |
| Device state | Unregistered |
| Device identifier | Not available |
| Error code | `53003` |
| Sign-in result | Failed |
| Policy | `Block-NonCompany-Devices` |
| Grant control | Block |
| Policy result | Failure |
| Previous Lab 06 policy | Disabled |

## Result interpretation

**Completed — policy-specific block for the unregistered test device verified.**

The Conditional Access tab identifies `Block-NonCompany-Devices` with Grant = Block and Result = Failure. The same event shows the previous Lab 06 policy as Disabled, supporting attribution to the Lab 07 policy.

Error `53003` is consistent with a Conditional Access denial, but the policy-specific evaluation is the stronger evidence.

## Important limitation

The sign-in event reports the device as **Unregistered** and does not provide a device identifier. The test therefore demonstrates that the negative filter matched the unregistered device in this scenario. It does **not** demonstrate a device explicitly registered with ownership set to **Personal**.

## Evidence

See [screenshots/README.md](screenshots/README.md). The main evidence is:
- `02-device-ownership-filter-rule.png`
- `03-failed-microsoft-sign-in-error-53003.png`
- `05-conditional-access-block-noncompany-policy-failure.png`

## Cleanup

Leave the policy On only if continued blocking of Don Paul's browser access from devices not identified as Company-owned is intended. Otherwise turn it Off after evidence capture. Keep the administrator exclusion.
