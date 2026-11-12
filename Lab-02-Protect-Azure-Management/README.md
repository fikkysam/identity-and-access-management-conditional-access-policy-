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

| Setting | Configuration |
|---|---|
| Policy name | `Protect-Azure-Management` |
| Included users | Debbie O — dedicated test user |
| Excluded identities | Administrator account |
| Target resources | Azure Resource Manager |
| Grant control | Grant access; Require multifactor authentication |
| Conditions | None selected |
| Policy state during enforcement validation | On |

**Resource naming note:** The resource picker and the sign-in event both identified the target as **Azure Resource Manager**.

## Test procedure

1. Enable `Protect-Azure-Management` by setting its policy state to **On**.
2. Sign in to the Azure portal as the included test user.
3. Open the corresponding interactive sign-in event in Microsoft Entra sign-in logs.
4. Inspect the **Conditional Access** tab and locate `Protect-Azure-Management`.
5. Inspect **Authentication details** to verify whether the MFA requirement was satisfied.

## Validation results

The captured interactive sign-in event showed:

- User: `debbie@fikayo.onmicrosoft.com`
- Application: Azure Portal
- Resource: Azure Resource Manager
- Sign-in status: Success
- Policy: `Protect-Azure-Management`
- Grant control: MFA
- Conditional Access policy result: **Success**
- Authentication details: **Previously satisfied**; **Succeeded: Yes**; result detail indicates the MFA requirement was satisfied

### Interpretation

The sign-in log confirms that the Conditional Access policy evaluated successfully and that its MFA requirement was satisfied. The authentication details specifically report **Previously satisfied**. This means the MFA requirement was met by an earlier authentication step or session; this event does **not** prove that a new MFA prompt was displayed during this sign-in.

The evidence therefore supports the claim **“MFA requirement satisfied through Conditional Access”**, not **“a new MFA prompt was triggered.”**

## Security notes

- Keep the administrator exclusion in place while testing to reduce the risk of administrative lockout.
- Use a dedicated test identity and a non-production tenant for policy validation.
- No additional device, location, network, or client-app conditions were configured. This keeps the test focused on the MFA grant requirement for Azure Resource Manager.

## Status

**Configuration and enforcement-mode policy evaluation: validated.** The sign-in log shows a successful `Protect-Azure-Management` evaluation with the MFA grant requirement satisfied. Authentication details indicate that MFA was previously satisfied rather than newly prompted in this event.

## Evidence

See [screenshots/README.md](screenshots/README.md) for the eight original configuration/report-only screenshots and the two additional enforcement-validation screenshots.
