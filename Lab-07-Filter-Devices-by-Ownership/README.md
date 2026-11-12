# Lab 07 — Filter Devices by Ownership

## Objective

Use Microsoft Entra Conditional Access **Filter for devices** to block browser access when a device is not identified as company-owned.

## Policy configuration

| Setting | Observed/configured value |
|---|---|
| Policy name | `Block-NonCompany-Devices` |
| Included identity | Don Paul (`don@fikayo.onmicrosoft.com`) |
| Excluded identity | Administrator account |
| Target resources | All resources (formerly All cloud apps) |
| Client app | Browser |
| Filter mode | Include filtered devices in policy |
| Device property | `deviceOwnership` |
| Operator | Not equals |
| Value | `Company` |
| Filter expression | `device.deviceOwnership -ne "Company"` |
| Grant control | Block access |
| Policy state at enforcement test | On |

The previous Lab 06 policy, `restrict windows Access`, was shown as Disabled in the same sign-in event's Conditional Access tab. This avoids attributing the Lab 07 test result to the previous policy.

## Test procedure and observed result

A browser sign-in to **My Apps** was attempted as Don Paul from the Windows workstation on November 12, 2026.

Microsoft sign-in troubleshooting details showed:
- Error code: `53003`
- Application: My Apps
- Device platform reported by Entra: Windows 10
- Device state: Unregistered
- Device identifier: Not available

The Conditional Access tab for the matching sign-in event showed:
- Policy: `Block-NonCompany-Devices`
- Grant control: **Block**
- Result: **Failure**
- Previous Lab 06 policy `restrict windows Access`: **Disabled**

This policy-specific evaluation is the evidence that the Lab 07 policy caused the block. Error 53003 is consistent with a Conditional Access denial, while the Conditional Access tab identifies the actual policy and control result.

## Why the negative ownership operator was used

Microsoft Entra evaluates device filter rules using device authentication. For an unregistered device, its device properties are considered null because the device object is not present in the directory. Microsoft documents that negative operators such as NotEquals can match unregistered devices, whereas positive operators do not.

Therefore, the expression:

```text
device.deviceOwnership -ne "Company"
```

matches devices not identified as Company-owned, including this unregistered test workstation. It does **not** positively establish that the workstation is classified as Personal. Testing a device explicitly registered with ownership set to Personal would be a separate validation scenario.

Reference: [Microsoft Learn — Filter for devices as a condition in Conditional Access](https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-condition-filters-for-devices)

## Outcome

**Completed — policy-specific Windows browser block verified.**

The matching sign-in event shows the named Lab 07 policy with Block / Failure. The sign-in details classify the device as unregistered and the platform as Windows 10, even though the physical workstation used for the test was Windows 11.

## Evidence

See the `screenshots/` folder and its evidence index. Evidence includes:
- All resources target selection
- Device filter mode and exact ownership rule
- Failed sign-in event
- Microsoft sign-in error 53003 and unregistered device details
- Conditional Access tab showing `Block-NonCompany-Devices` with Block / Failure and Lab 06 disabled

## Security scope and cleanup

This policy applies to the selected test user, Browser client, and all targeted resources when the device filter matches. The administrator account remains excluded.

Leave the policy On only if you intend to continue blocking Don Paul's browser access from devices not identified as company-owned. Otherwise, switch it Off after capturing evidence. Do not remove the administrator exclusion while the policy is enabled.
