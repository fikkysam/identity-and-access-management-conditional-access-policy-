# Lab 01 — Test Results

## Test execution

A Microsoft Graph PowerShell device-code sign-in was initiated using:

```powershell
Connect-MgGraph -UseDeviceAuthentication -Scopes "User.Read" -ContextScope Process
```

The Microsoft Graph context was checked using:

```powershell
Get-MgContext | Select-Object Account, AuthType, Scopes
```

The context output identified the dedicated test user and a delegated Microsoft Graph connection.

## Sign-in log evaluation

The relevant event was identified under **User sign-ins (interactive)** for the test identity and the **Microsoft Graph Command Line Tools** application. The sign-in event targeted Microsoft Graph.

The Conditional Access policy details showed:

| Evaluation item | Observed result |
|---|---|
| Test user | Matched |
| Resource | Microsoft Graph — Matched |
| Authentication flows | Matched |
| Grant control | Block |
| Report-only policy result | Report-only: Failure |

## Interpretation

The event matched the policy's user, resource, and device-code authentication-flow scope. The Block grant control was evaluated. The Report-only Failure result indicates that the Conditional Access policy would have blocked access if the policy were enabled.

Because the policy remained in Report-only mode, this policy did not enforce the block. The successful Microsoft Graph connection is therefore consistent with a Report-only evaluation.

## Result

**Lab 01: Test evaluation passed.**

The configured policy was saved, the matching device-code sign-in was generated, and the sign-in logs showed the expected policy evaluation.

## Limitations and follow-up

- The policy remains in Report-only mode; enforcement was not tested.
- The test was performed against the selected test identity and Microsoft Graph resource.
- A separate sign-in event may show a different evaluation. Evidence must refer to the same test-user device-code event.
- Authentication details may not always expose a separate authentication event record. The sign-in's Conditional Access evaluation and Authentication flows condition were used to verify the flow match.

## Evidence checklist

- [x] Saved policy overview showing Report-only state, included test user, excluded identity, target resources, grant and authentication flow.
- [x] Policy creation/configuration view showing the included test user and Report-only selection.
- [x] Excluded administrator identity view.
- [x] Authentication flows configuration showing Device code flow selected.
- [x] Sign-in event for the test user and Microsoft Graph Command Line Tools.
- [x] Conditional Access policy details showing Authentication flows matched and Block grant control.
- [x] Report-only evaluation showing Report-only: Failure.
