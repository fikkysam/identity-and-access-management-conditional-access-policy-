# Lab 02 — Configuration

## Prerequisites

- A Microsoft Entra tenant with Conditional Access capability.
- A dedicated test user.
- A separate administrator and emergency access account excluded from the policy.
- Azure management target resource available in the tenant.

## Policy details

| Setting | Value |
|---|---|
| Policy name | `Protect-Azure-Management` |
| Users — Include | Dedicated test user: Debbie O |
| Users — Exclude | Administrator account |
| Target resources | Select resources → Azure Resource Manager |
| Conditions | None selected |
| Grant | Grant access |
| Grant requirement | Require multifactor authentication |
| Enable policy | Report-only |

## Configuration procedure

1. Sign in to the Microsoft Entra admin center at https://entra.microsoft.com/ using the administrator account.
2. Navigate to **Conditional Access → Policies → New policy**.
3. Name the policy `Protect-Azure-Management`.
4. Under **Users**, include the dedicated test user, Debbie O.
5. Under **Exclude**, exclude the administrator account and ensure emergency access accounts are not targeted.
6. Under **Target resources**, choose **Resources (formerly cloud apps)** and **Select resources**.
7. Search for the Azure management resource. In this tenant's picker, the selected entry was **Azure Resource Manager**. Select it and confirm that one resource is included.
8. Leave **Conditions** unconfigured for this exercise.
9. Under **Access controls → Grant**, select **Grant access** and check **Require multifactor authentication**.
10. Set **Enable policy** to **Report-only**.
11. Review the user scope, resource, grant control, and exclusions, then create the policy.
12. Open the saved policy details and confirm its state is Report-only and its access requirement is Require multifactor authentication.

## Important resource naming clarification

The practical-labs guide labels the target resource **Microsoft Azure Management**. The tenant's resource picker did not return that exact display name. Searching for `windows` returned Windows 365 and Windows Azure Active Directory; neither was selected. The tenant's picker showed **Azure Resource Manager**, which was selected instead. The subsequent sign-in event identified its resource as Azure Resource Manager, so the configured resource and test event matched.

Do not substitute **Windows Azure Active Directory** or **Windows 365** for the Azure management resource.

## Safety controls

- Keep the policy in Report-only while validating the match and evaluation.
- Keep administrator and emergency access identities excluded.
- Do not switch the policy to On as part of this lab's Report-only validation.
- Use a dedicated test identity rather than a production administrator account.
