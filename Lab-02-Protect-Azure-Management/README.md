# Lab 02 — Protect Azure Management

## Objective

Apply a dedicated multifactor authentication (MFA) access requirement when a designated test user accesses Azure management resources.

## Security context

Azure management access can expose administrative operations over Azure resources. Requiring MFA for management access adds an authentication control to this sensitive access path.

## Lab environment

- Microsoft Entra ID non-production tenant
- Administrator account used to configure Conditional Access and review sign-in logs
- Dedicated test identity: Debbie O (`debbie@fikayo.onmicrosoft.com`)
- Azure portal sign-in used to generate a management-resource sign-in event

## Policy configuration

| Setting | Observed configuration |
|---|---|
| Policy name | `Protect-Azure-Management` |
| Included users | 1 user — Debbie O |
| Excluded identities | 1 user — administrator account |
| Target resources | 1 resource — Azure Resource Manager |
| Grant control | Grant access; Require multifactor authentication |
| Conditions | None selected |
| Policy state | Report-only |

**Resource naming note:** The lab guide describes the target as Microsoft Azure Management. In the tenant's current resource picker, the selected resource was displayed as **Azure Resource Manager**. The sign-in event used for validation also showed **Azure Resource Manager** as its resource. This is the resource actually configured and tested in this lab.

## Test approach

1. Sign in to the Azure portal as the dedicated test user.
2. Access the Azure portal and generate a sign-in event for Azure Resource Manager.
3. Open the matching interactive sign-in event in Microsoft Entra sign-in logs.
4. Inspect the Report-only tab and locate `Protect-Azure-Management`.
5. Record the grant control and policy evaluation result.

See [configuration.md](configuration.md) and [test-results.md](test-results.md) for the procedure and observed evidence.

## Outcome

The fresh interactive sign-in event showed:
- User: `debbie@fikayo.onmicrosoft.com`
- Application: Azure Portal
- Resource: Azure Resource Manager
- Sign-in status: Success
- Conditional Access Report-only policy: `Protect-Azure-Management`
- Grant control: MFA
- Displayed result: **Report-only: User action required** (the result text was truncated in the screenshot)

This confirms that the policy appeared in the Report-only evaluation for the matching user/resource event and that the MFA grant control was evaluated. The displayed result indicates additional user interaction would be required for the MFA control. Because the policy is Report-only, it did not enforce an MFA challenge.

## Status

**Lab 02 configuration and policy matching: completed.** The policy remains in Report-only mode. Enforced MFA was not tested.

## Evidence screenshots

The following links point directly to the screenshot files currently stored in the repository:

- [Excluded user](screenshots/excluded%20user)
- [Included user](screenshots/included%20user)
- [Target resource selection](screenshots/Target%20resource%20name)
- [Grant policy](screenshots/Grant%20policy)
- [Screenshot 05](screenshots/Screenshot%202026-11-10%20202722.png)
- [Screenshot 06](screenshots/Screenshot%202026-11-10%20202827.png)
- [Screenshot 07](screenshots/Screenshot%202026-11-10%20203834.png)
- [Screenshot 08](screenshots/Screenshot%202026-11-10%20204727.png)
- [Screenshot 09](screenshots/Screenshot%202026-11-10%20204936.png)
- [Screenshot 10](screenshots/Screenshot%202026-11-10%20205346.png)

See the [screenshot index](screenshots/README.md) for the complete evidence list.
