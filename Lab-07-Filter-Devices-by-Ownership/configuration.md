# Lab 07 — Configuration

## Prerequisites

- Non-production Microsoft Entra tenant.
- Dedicated test identity: Don Paul (`don@fikayo.onmicrosoft.com`).
- Separate administrator account excluded from the policy.
- Conditional Access policy management and sign-in log access.

## Policy configuration

| Setting | Configured value |
|---|---|
| Policy name | `Block-NonCompany-Devices` |
| Users included | Don Paul (`don@fikayo.onmicrosoft.com`) |
| Users excluded | Administrator account |
| Target resources | All resources (formerly All cloud apps) |
| Client app | Browser |
| Filter mode | Include filtered devices in policy |
| Device property | `deviceOwnership` |
| Operator | Not equals |
| Value | `Company` |
| Filter expression | `device.deviceOwnership -ne "Company"` |
| Grant | Block access |
| Policy state during test | On |

## Configuration procedure

1. Open **Microsoft Entra admin center → Protection → Conditional Access → Policies**.
2. Create or open `Block-NonCompany-Devices`.
3. Include Don Paul and exclude the administrator account.
4. Target **All resources**.
5. Under **Conditions → Client apps**, select Browser.
6. Under **Conditions → Filter for devices**, enable the filter.
7. Select **Include filtered devices in policy**.
8. Configure the device property `deviceOwnership`, operator **Not equals**, and value `Company`.
9. Confirm the expression is `device.deviceOwnership -ne "Company"`.
10. Under **Grant**, select **Block access**.
11. Set the policy to **On** for the controlled test and save.

## Filter semantics

The negative ownership operator is material to this test. For an unregistered device, device properties can be null because there is no corresponding device object in the directory. A negative operator such as NotEquals can match such a device.

The observed test device was **Unregistered**. This does not prove that Entra classified it as **Personal**. A separately registered device whose ownership property is explicitly set to Personal would be a different validation case.

Reference: [Microsoft Learn — Filter for devices as a condition in Conditional Access](https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-condition-filters-for-devices)

## Policy interaction

The previous Lab 06 policy, `restrict windows Access`, appeared as Disabled in the Lab 07 sign-in event. This helps isolate the Lab 07 policy as the policy responsible for the observed block.

## Evidence

See [screenshots/README.md](screenshots/README.md) for the five-item evidence index.
