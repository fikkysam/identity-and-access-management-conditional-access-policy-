# Lab 09 — Conditional Access App Control

## Objective

Use Microsoft Entra Conditional Access and Microsoft Defender for Cloud Apps (Defender for Cloud Apps) to route a supported browser session through the Defender session-control proxy and block file downloads from SharePoint Online.

## Environment and prerequisites

- Microsoft Entra ID P2 was available in the tenant.
- A Microsoft 365 E5 trial was activated to provide the Defender for Cloud Apps entitlement used for this lab.
- The E5 trial licence was assigned to the dedicated test user.
- Microsoft Defender for Cloud Apps was available in the Microsoft Defender portal.
- SharePoint Online was used as the supported cloud application.
- A dedicated test identity was used; the administrator identity was excluded from the Conditional Access policy.
- Testing used a harmless text file in a non-production SharePoint document library.

> **Licensing note:** Entra ID P2 by itself does not provide every Defender for Cloud Apps session-control capability. Confirm the applicable Defender for Cloud Apps entitlement, service availability, and app support before reproducing this lab in another tenant.

## Conditional Access configuration

| Setting | Implemented value |
|---|---|
| Policy name | `Microsoft Defender App Control` |
| Policy state | **On** |
| Included identity | Dedicated test user: Debbie O |
| Excluded identity | Administrator account |
| Target resource | Office 365 |
| Client app | Browser |
| Grant controls | None configured |
| Session control | Use Conditional Access App Control |
| App-control mode | **Block downloads (Preview)** |

The resource scope is **Office 365**, not only SharePoint Online. The policy was limited to the dedicated test user and browser client. Because Office 365 is a broad resource selection, review the scope carefully before adapting this configuration for a production user.

## Implementation and test procedure

1. Confirm the Defender for Cloud Apps entitlement and open the Microsoft Defender portal.
2. Create the Conditional Access policy in Microsoft Entra admin center.
3. Include the dedicated test user and exclude the administrator identity.
4. Target Office 365 and the Browser client app.
5. Under **Session**, select **Use Conditional Access App Control** and choose **Block downloads (Preview)**.
6. Set the policy state to **On** and create the policy.
7. Open a fresh Microsoft Edge InPrivate session and sign in to SharePoint Online as Debbie O.
8. Navigate to the Communication site's **Documents** library.
9. Create and save a harmless test file named `iam-lab.txt`.
10. Attempt to download the file from the SharePoint browser session.
11. Verify the browser result and inspect the Defender for Cloud Apps Activity log.
12. Open the event's **Matched policies** details to identify the policy responsible for the session-control action.

## Observed results

### Browser enforcement

- SharePoint access was routed through the Defender for Cloud Apps proxy. The browser URL used the tenant's `access.mcas.ms` proxy host.
- The test file `iam-lab.txt` was saved successfully in the SharePoint Documents library.
- When the test user selected Download, Defender displayed **Download blocked** and stated that downloading `iam-lab.txt` was blocked by the organisation's security policy.
- Edge showed a generated `Blocked_...txt` response instead of delivering the original test file.

### Defender Activity log

The Defender for Cloud Apps Activity log recorded the event with these details:

| Field | Observed value |
|---|---|
| Activity | Download file |
| File | `iam-lab.txt` |
| App | Microsoft SharePoint Online |
| Source | **Session control** |
| Event time | November 13, 2026, 8:43 PM (tenant/session local display) |
| Matched policy | **Microsoft Defender App Control** |
| Policy configuration source | Microsoft Entra ID |

Opening **Matched policies** displayed **Microsoft Defender App Control** with the note **Configured in Microsoft Entra ID**.

## Validation outcome

**Completed — enforcement and policy attribution verified.**

The lab's primary control objective was verified end to end:

1. The test browser session reached SharePoint through the Defender for Cloud Apps proxy.
2. The download attempt was blocked in the SharePoint browser session.
3. Defender recorded the download activity with source **Session control**.
4. Defender attributed the event to the **Microsoft Defender App Control** policy configured in Microsoft Entra ID.

The blocked-download screen, Activity log event, and Matched policies dialog provide separate corroborating evidence. The Activity log event is especially important because it ties the observed block to session control and identifies the policy.

## Troubleshooting notes

- The Microsoft 365 launcher initially returned an `ERR_TOO_MANY_REDIRECTS` error. Opening the tenant's SharePoint site directly resolved the navigation issue.
- The initial Defender access notification used the wording **monitor mode**. That notification alone was not treated as proof of the final download-control result. The actual download attempt was blocked, and the corresponding Activity log event showed **Source: Session control** and the matched Entra policy.
- The Activity log's suggested-query menu and its filter menu are different controls. The download event was located through the query interface and then expanded to inspect its details.
- If a similar test does not block downloads, verify the policy state, included/excluded identities, target resource, Browser client condition, selected session control, licensing, and supported-app routing.

## Security and cleanup considerations

- Keep the policy scoped to a dedicated test identity until production impact is understood.
- Maintain administrator and emergency-access exclusions.
- Use non-sensitive test data.
- Review the broad **Office 365** resource scope before extending the policy to additional users.
- Remove the test file from the SharePoint Documents library when it is no longer needed.
- Review trial subscription settings separately; do not assume that a trial automatically stops billing.

## Evidence

The lab was validated using the following portal evidence captured during the test:

1. Entra Conditional Access policy details showing the policy **On**, one included identity, one excluded identity, one included resource, and Conditional Access App Control as the access requirement.
2. SharePoint's **Download blocked** result for `iam-lab.txt`.
3. Defender Activity log event showing the download activity and **Source: Session control**.
4. Defender **Matched policies** dialog identifying **Microsoft Defender App Control** as configured in Microsoft Entra ID.

