# Lab 05 — Protect Device Registration and Join

## Objective

Use Microsoft Entra Conditional Access to require multifactor authentication (MFA) when a test user registers or joins a device to the tenant.

This lab focuses on the Conditional Access **User actions** target, specifically **Register or join devices**. It is not an Office 365 or Azure Resource Manager cloud-app targeting exercise.

## Environment and safety

- Microsoft Entra non-production lab tenant
- Dedicated test identity: Don Paul (the account selected in the policy)
- Separate administrator account, excluded from the policy
- Windows 11 Pro test VM required for the end-to-end device registration test
- Do not use a production device or the primary administrator identity for testing
- Keep the policy in Report-only mode until its evaluation has been reviewed

## Policy configuration

| Setting | Configuration |
|---|---|
| Policy name | `Require MFA for Device Registration` |
| Users — Include | Don Paul (dedicated test identity) |
| Users — Exclude | Administrator account |
| Target resources | User actions |
| User action | Register or join devices |
| Grant | Grant access |
| Grant control | Require multifactor authentication |
| Initial policy state | Report-only |

The policy was created successfully with the settings above. Configuration screenshots will be added to the `screenshots/` folder.

## End-to-end test procedure (pending)

The end-to-end test could not be completed in the current lab environment because the available VM setup did not permit adding/using the required separate Entra test identity for device registration. The steps below document how the test will be performed when a suitable test VM is available.

1. Prepare a Windows 11 Pro VM with internet access. Use a disposable lab VM that is not already joined or registered to the target Entra tenant.
2. Sign in to Windows using the VM's existing Windows account. A separate Windows local login is not required solely to assign the Conditional Access policy.
3. Open **Settings → Accounts → Access work or school → Connect**.
4. Select **Join this device to Microsoft Entra ID** 
5. At the organisation sign-in prompt, enter the dedicated Entra test user's credentials (Don Paul), not the administrator credentials.
6. Complete the MFA prompt if one is presented, then follow the remaining prompts to attempt the device join.
7. Record whether registration/join succeeds or is blocked.
8. In Microsoft Entra admin center, open **Monitoring & health → Sign-in logs**, locate the test user's relevant event, and inspect its **Conditional Access** tab.
9. Find `Require MFA for Device Registration` and record the Report-only evaluation result and the MFA grant-control result. Review authentication details as well: an earlier satisfied MFA claim may satisfy the requirement without a fresh prompt during that particular sign-in.
