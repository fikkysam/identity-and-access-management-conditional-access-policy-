# Lab 03 — Require Terms of Use Acceptance

## Objective

Require users to accept an organizational Terms of Use agreement before accessing a protected cloud resource.

## Security context

A Terms of Use (ToU) control presents an organizational acceptable-use agreement during sign-in. The user must accept the agreement before access is granted when the Conditional Access policy is enforced.

## Lab environment

- Microsoft Entra ID non-production tenant
- Separate administrator account used to configure the policy and review logs
- Test identity used to access the protected resource
- Entra Terms of Use document uploaded as a PDF

## Policy configuration

| Setting | Observed configuration |
|---|---|
| Policy name | `use of acceptance policy` |
| Target resource | Office 365 (1 resource included) |
| Grant control | Use-Agreement |
| Multiple grant controls | Require one of the selected controls |
| Session controls | 0 controls selected |
| Policy state | On |

The captured policy view shows the **Use-Agreement** grant control selected and the policy enabled. The Terms of Use document is named **acceptance use of policy**.

## Test procedure

1. Sign in to the protected resource using the test identity.
2. Open the Terms of Use prompt.
3. Expand and read the agreement, then select **Accept**.
4. Return to Microsoft Entra sign-in logs and inspect the corresponding sign-in event.
5. Open the Terms of Use audit log and verify the acceptance event.

## Outcome

The captured evidence shows:

- The user was presented with the **fikayo terms of use** page.
- The agreement **acceptance use of policy** was displayed.
- The user selected **Accept**.
- The Conditional Access sign-in event listed `use of acceptance policy` with the **Use-Agreement** grant control and a **Success** result.
- The Terms Of Use audit log recorded **Accept Terms Of Use** with **Success** status.

This supports that the agreement was accepted and the Terms of Use control succeeded for the observed sign-in.

## Status

**Lab 03: completed — acceptance and sign-in evidence captured.**

## Evidence

See [screenshots/README.md](screenshots/README.md) for the evidence index. Screenshots should be uploaded to this folder before the repository is considered to contain the complete visual evidence set.

## Notes and limitations

- The evidence confirms the observed acceptance and successful policy evaluation; it does not independently establish the legal validity of the agreement.
- The policy is enabled in the captured configuration. Keep this type of enforcement limited to the intended test scope in a non-production tenant.
- Do not publish real legal agreements or sensitive organizational terms without authorization.
