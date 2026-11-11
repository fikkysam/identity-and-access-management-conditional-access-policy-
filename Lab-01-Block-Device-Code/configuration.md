# Lab 01 — Configuration

## Prerequisites

- Microsoft Entra tenant with Conditional Access capability.
- Dedicated test user.
- Separate administrator account with appropriate permissions to create Conditional Access policies and read sign-in logs.
- Microsoft Graph PowerShell SDK and a client capable of initiating device-code authentication.

## Policy configuration steps

1. Sign in to the Microsoft Entra admin center using the administrator account.
2. Open **Entra ID → Conditional Access → Policies** and create a new policy.
3. Name it `Block-device-Authentication`.
4. Under **Users and groups → Include**, select only the dedicated test user.
5. Under **Users and groups → Exclude**, exclude the administrator account and any emergency access account.
6. Under **Target resources**, select **All resources** for this lab.
7. Open **Conditions → Authentication flows**.
8. Set **Configure** to **Yes** and select **Device code flow**. Do not select unrelated flows.
9. Under **Access controls → Grant**, select **Block access**.
10. Set **Enable policy** to **Report-only**, then create/save the policy.

## Test command

Run the following in PowerShell:

```powershell
Connect-MgGraph -UseDeviceAuthentication -Scopes "User.Read" -ContextScope Process
```

Complete the device login using the dedicated test account, not the administrator account.

Verify the active Graph context:

```powershell
Get-MgContext | Select-Object Account, AuthType, Scopes
```

The account shown should be the dedicated test user. Do not record or publish the temporary device code, access token, or other credentials.

## Expected policy evaluation

For a sign-in that matches the policy scope and Device code flow condition:
- The test user and target resource should match.
- Authentication flows should show **Matched**.
- The Block grant control should be evaluated.
- The Report-only tab should show **Report-only: Failure** if the policy would block the sign-in.

## Administrative separation

Use the administrator account for policy configuration and sign-in log review. Use the dedicated test account only to generate the authentication event being tested.
