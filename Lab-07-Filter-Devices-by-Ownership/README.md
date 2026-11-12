# Lab 07 — Filter Devices by Ownership

## Objective

Use the Microsoft Entra Conditional Access **Filter for devices** condition to block access from devices that are not identified as company-owned.

The lab uses a deliberately broad non-company rule:

```
device.deviceOwnership -ne "Company"
```

This rule matches devices whose ownership is `Personal` and also unregistered devices, whose device properties are evaluated as null. It is chosen because the current test workstation was reported as **Unregistered** in the Lab 06 sign-in details. A positive rule such as `device.deviceOwnership -eq "Personal"` would not match an unregistered device.

## Planned policy

| Setting | Value |
|---|---|
| Policy name | `CA07-Block-NonCompany-Devices` |
| Users — Include | Don Paul (`don@fikayo.onmicrosoft.com`) |
| Users — Exclude | Administrator account |
| Target resources | All resources |
| Client apps | Browser |
| Filter for devices — Configure | Yes |
| Devices matching the rule | Include filtered devices in policy |
| Filter rule | `device.deviceOwnership -ne "Company"` |
| Grant | Block access |
| Policy state | Report-only during setup; On for the single enforcement test |

## Important preparation

**Turn off the Lab 06 policy before testing Lab 07.** Lab 06 blocks Don Paul's Windows browser access to all targeted resources. If it remains On, it can independently block the Lab 07 test and make attribution ambiguous.

1. Open Entra ID → Conditional Access → Policies.
2. Open `restrict windows Access` (Lab 06).
3. Set Enable policy to **Off** and save. Do not delete the policy or its evidence.
4. Confirm the Lab 06 policy is Off before proceeding.

## Configuration procedure

1. Open Microsoft Entra admin center → Entra ID → Conditional Access → Policies → New policy.
2. Name the policy `CA07-Block-NonCompany-Devices`.
3. Under Users, include only Don Paul. Under Exclude, keep the administrator account excluded.
4. Under Target resources, select All resources for this controlled lab scenario.
5. Under Conditions → Client apps, configure **Browser** only.
6. Under Conditions → Filter for devices, set Configure to **Yes**.
7. Select **Include filtered devices in policy**.
8. Use the rule builder or rule syntax to enter exactly:
   `device.deviceOwnership -ne "Company"`
9. Under Access controls → Grant, select **Block access**.
10. Keep the policy in Report-only while checking the configuration. Before the single enforcement test, change the policy to **On** and save. Do not perform a separate Report-only sign-in test.
11. Verify the administrator exclusion is still present before testing.

## Single enforcement test

1. Use a browser on the Windows workstation used in Lab 06.
2. Open an Incognito/InPrivate window.
3. Navigate to `https://myapps.microsoft.com`.
4. Sign in as Don Paul (`don@fikayo.onmicrosoft.com`).
5. Record the actual result. With the current device reported as unregistered, the negative ownership operator is expected to match the null ownership attribute and the policy is expected to block the sign-in.
6. In Entra admin center, open Monitoring & health → Sign-in logs.
7. Locate the matching interactive sign-in for Don Paul and open its Conditional Access tab.
8. Confirm that `CA07-Block-NonCompany-Devices` appears with Grant control **Block** and Result **Failure**. Record the event time, application, device details, and correlation ID.

## Interpretation and limitations

Microsoft Entra evaluates device filter rules using device authentication. For an unregistered device, device properties are null. Positive operators (for example, `-eq "Personal"`) do not match an unregistered device; negative operators (for example, `-ne "Company"`) do.

This exercise therefore validates a **non-company / not-known-to-be-company-owned** rule. It does not prove the workstation is positively classified as Personal. To validate the Personal and Company values separately, use registered devices whose `device.deviceOwnership` values are explicitly Personal and Company.

The policy targets all resources for one test user and the Browser client. The administrator is excluded. Leave Lab 07 On only if you intend to continue blocking Don Paul's browser access from non-company or unregistered devices. Otherwise, turn it Off after evidence capture.

## Evidence checklist

Capture the following screenshots:

- Lab 06 policy switched Off before the Lab 07 test.
- Lab 07 user inclusion and administrator exclusion.
- Target resources and Browser client condition.
- Filter for devices configured with Include filtered devices in policy.
- Exact filter rule: `device.deviceOwnership -ne "Company"`.
- Block access grant and policy enabled state.
- Microsoft sign-in result.
- Matching sign-in log's Conditional Access tab showing this policy's Block / Failure result.

## Cleanup

After evidence capture, decide whether to leave the policy On as a demonstration or turn it Off. Do not remove the administrator exclusion while the policy is enabled.
