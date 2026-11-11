# Lab 03 — Configuration

## Prerequisites

- Microsoft Entra tenant with Conditional Access and Terms of Use capability.
- An approved test Terms of Use PDF.
- A dedicated test identity.
- A separate administrator account for policy configuration and audit review.
- A protected cloud resource available in the tenant.

## Terms of Use document

The tenant's Terms of Use page displayed the agreement named:

`acceptance use of policy`

The user-facing page displayed the heading **fikayo terms of use** and required the user to accept the agreement before proceeding.

## Conditional Access policy

| Setting | Observed value |
|---|---|
| Policy name | `use of acceptance policy` |
| Target resources | Select resources → Office 365 |
| Resource count | 1 resource included |
| Grant control | Use-Agreement |
| Multiple controls | Require one of the selected controls |
| Session controls | 0 controls selected |
| Enable policy | On |

## Configuration procedure

1. Sign in to the Microsoft Entra admin center using the administrator account.
2. Navigate to **Conditional Access → Terms of use**.
3. Create or select the approved Terms of Use document and upload the PDF.
4. Configure the display name and acceptance settings, then save the document.
5. Navigate to **Conditional Access → Policies** and create the policy named `use of acceptance policy`.
6. Configure the intended test-user scope. Keep administrator and emergency access accounts out of the policy scope.
7. Under **Target resources**, select the intended cloud resource. The captured policy selected **Office 365** and showed one resource included.
8. Under **Access controls → Grant**, select **Grant access** and enable the **Use-Agreement** control.
9. For multiple controls, the captured configuration selected **Require one of the selected controls**.
10. Leave Session controls unconfigured for this exercise.
11. Enable the policy for the controlled Terms of Use acceptance test, after verifying the policy scope and recovery access.
12. Save the policy.

## Test procedure

1. Sign in as the test identity and access the targeted resource.
2. Confirm that the Terms of Use page is displayed.
3. Expand the agreement and review its contents.
4. Select **Accept**.
5. Verify the corresponding sign-in event under **Monitoring & health → Sign-in logs**.
6. Verify the acceptance record under **Audit logs**, filtering for the Terms Of Use service and the Accept Terms Of Use activity.

## Safety and scope

- Use a non-production tenant and a test identity.
- Verify administrator and emergency access exclusions before enabling the policy.
- Only upload an agreement that is approved for this lab.
- Do not publish confidential legal or organizational content.
