# Lab 10 — Continuous Access Evaluation (CAE)

## Objective

Observe a CAE-capable SharePoint Online session before and after an administrator explicitly revokes a user's sessions. Record the CAE sign-in indicator, Entra audit event, failed reauthentication attempt, and subsequent access recovery without overstating what the logs prove.

## Environment and prerequisites

- Microsoft Entra ID tenant with sign-in and audit log access.
- SharePoint Online, which is among the initial workloads supported by CAE.
- Dedicated test identity: Debbie O (debbie@fikayo.onmicrosoft.com).
- Separate administrator identity to perform the session revocation.
- Non-production SharePoint Communication site and Documents library.
- Harmless test file: iam-lab.txt.
- Lab 09's Defender App Control policy was temporarily disabled during the clean-session portion of this test and restored to **On** afterward.

## Technical background

Continuous Access Evaluation (CAE) allows supported resource providers, including SharePoint Online, to evaluate certain critical events during an active session rather than relying only on normal access-token expiry. One supported critical event is an administrator explicitly revoking all refresh tokens for a user.

The Entra sign-in logs expose a **Continuous access evaluation** field and an **Is CAE Token** filter. Microsoft notes that an authentication can generate multiple sign-in requests and only one request may be marked as CAE; it can appear in either the interactive or non-interactive tab.

References:
- [Continuous access evaluation in Microsoft Entra](https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-continuous-access-evaluation)
- [Monitor and troubleshoot CAE sign-ins](https://learn.microsoft.com/en-us/entra/identity/conditional-access/howto-continuous-access-evaluation-troubleshoot)
- [Microsoft Entra authentication and authorization error codes](https://learn.microsoft.com/en-us/entra/identity-platform/reference-error-codes)

## Test configuration

| Item | Value |
|---|---|
| Resource | SharePoint Online |
| Browser | Microsoft Edge |
| Test identity | Debbie O |
| Administrator action | Revoke sessions |
| Critical event audit operation | Update StsRefreshTokenValidFrom Timestamp |
| Test file | iam-lab.txt |

## Implementation and test procedure

1. Temporarily turn off the Lab 09 **Microsoft Defender App Control** Conditional Access policy to establish a clean, non-proxied SharePoint session for this test.
2. Open a new Edge InPrivate window and sign in to SharePoint Online as Debbie O.
3. Open the Communication site's Documents library and open iam-lab.txt to establish an active SharePoint browser session.
4. In a separate administrator session, open Debbie O's user profile in Microsoft Entra admin center.
5. Select **Revoke sessions** and confirm the action. The portal displayed a success notification.
6. Return to Debbie's existing SharePoint browser session and refresh the open resource. The browser was redirected to Microsoft sign-in and prompted for Debbie's password.
7. In Entra **Sign-in logs**, filter for Debbie and inspect the successful SharePoint Online sign-in where **Is CAE Token = Yes**.
8. Inspect the failed SharePoint sign-in that followed the revocation and record the CAE field, error code, failure reason, and additional details.
9. In Entra **Audit logs**, inspect the corresponding **Update StsRefreshTokenValidFrom Timestamp** event and verify Debbie is the target.
10. Reauthenticate Debbie and confirm the SharePoint Documents library becomes accessible again.
11. Restore the Lab 09 **Microsoft Defender App Control** policy to **On** and verify the setting.

## Observed results

### 1. CAE-capable SharePoint sign-in

The successful interactive SharePoint Online sign-in at **November 14, 2026, 03:53:46 UTC** showed:

- Status: **Success**
- Continuous access evaluation: **Yes**
- Authentication requirement: Single-factor authentication
- Additional details: MFA requirement satisfied by claim in the token

The Entra **Is CAE Token = Yes** filter also returned successful SharePoint Online sign-ins in the interactive tab. No matching records were returned in the non-interactive tab for the same filter and time range.

### 2. Administrator-initiated session revocation

The administrator selected **Revoke sessions** for Debbie O. The portal displayed **Successfully revoked sign-in sessions**.

The Entra Audit log then recorded:

| Field | Observed value |
|---|---|
| Service | Core Directory |
| Category | UserManagement |
| Activity type | Update StsRefreshTokenValidFrom Timestamp |
| Status | **Success** |
| Time | November 13, 2026, 9:57 PM (local portal time) |
| Target | Debbie O — debbie@fikayo.onmicrosoft.com |

The event's **Target(s)** tab confirmed Debbie O's user principal name.

### 3. Existing SharePoint session prompted for reauthentication

After the administrator revocation, the existing SharePoint browser session redirected Debbie to Microsoft sign-in and displayed an **Enter password** prompt.

The subsequent SharePoint sign-in event at **November 14, 2026, 03:58:58 UTC** showed:

| Field | Observed value |
|---|---|
| Application | Office 365 SharePoint Online |
| Status | **Failure** |
| Sign-in error code | **50133 — SsoArtifactRevoked** |
| Continuous access evaluation | **No** |
| Failure reason | Session not valid due to password expiration or recent password change |
| Additional details | Refresh tokens and sessions can expire or be revoked by the user or an administrator; the app requests a new login |

The event occurred shortly after the successful audit operation. The 50133 result is consistent with the revoked session artifact being rejected and the app requesting a new login.

### 4. Access recovery and policy restoration

After Debbie authenticated again, the SharePoint **Documents** library loaded and displayed iam-lab.txt. Lab 09's Defender App Control policy was subsequently confirmed **On**.

The file preview did not reopen after Lab 09's download-blocking policy was restored; the file was still visible in the library. That preview issue is not used as CAE validation evidence.

## Validation and interpretation

**Outcome: Completed — CAE-capable SharePoint sign-in, administrator-triggered session revocation, resource-session interruption, and reauthentication were observed and corroborated by Entra sign-in and audit logs.**

Evidence supports all of the following:

1. SharePoint Online issued a successful sign-in marked **Continuous access evaluation = Yes**.
2. The administrator successfully revoked Debbie's sessions.
3. Entra Audit logs recorded **Update StsRefreshTokenValidFrom Timestamp** with Debbie as the target.
4. The existing SharePoint session redirected to Microsoft sign-in.
5. A subsequent SharePoint sign-in attempt failed with **50133 — SsoArtifactRevoked**.
6. Debbie later authenticated again and the SharePoint Documents library loaded.

**Interpretation of the CAE sign-in flag:** The successful SharePoint sign-in showed **Continuous access evaluation = Yes**. The later failed sign-in showed **Continuous access evaluation = No** because it was a separate failed token/reauthentication request. Microsoft's CAE troubleshooting guidance explains that one authentication can generate multiple sign-in requests and only one request is marked as CAE; that record can appear in either the interactive or non-interactive tab. The CAE flag on the failed request therefore does not negate the CAE-capable token recorded on the successful SharePoint sign-in. The sequence of a CAE-capable session, supported administrator revocation event, SharePoint sign-in challenge, and **50133 — SsoArtifactRevoked** is consistent with Microsoft's documented CAE revocation flow. The browser's reauthentication prompt and the subsequent Entra failure are observed evidence; the underlying HTTP 401 claims-challenge payload was not separately captured.

## Troubleshooting notes

- Check both **User sign-ins (interactive)** and **User sign-ins (non-interactive)** when using the **Is CAE Token** filter. CAE may be marked on only one request associated with an authentication.
- Do not infer CAE from a password prompt alone. Correlate a successful CAE-token sign-in, the supported critical-event audit record, the interrupted resource session, and the subsequent authentication result.
- Error **50133** is identified by Microsoft as **SsoArtifactRevoked**; inspect the full failure reason and additional details in the event.
- Keep Lab 09's Defender App Control policy separate from the CAE experiment. Its **Block downloads** session control was restored after the clean-session test and may affect file preview/download actions.

## Security and cleanup

- Keep administrator operations in a separate administrator session.
- Use a dedicated test identity and non-sensitive SharePoint file.
- Do not reset Debbie's password or disable the account as part of this test.
- Restore any temporarily disabled security policy after testing. Lab 09's **Microsoft Defender App Control** policy was confirmed **On** after this test.
- Reauthenticate the test user after the revocation event if the account is to be used for subsequent labs.

## Evidence captured

1. Entra sign-in log filtered with **Is CAE Token = Yes**.
2. Successful SharePoint sign-in details showing **Continuous access evaluation = Yes**.
3. Failed SharePoint sign-in details showing error **50133**, failure reason, and **Continuous access evaluation = No**.
4. Audit Log Details showing **Update StsRefreshTokenValidFrom Timestamp** with **Status: success**.
5. Audit Log **Target(s)** tab showing debbie@fikayo.onmicrosoft.com.
6. SharePoint Documents library after Debbie reauthenticated.
7. Conditional Access policy details confirming Lab 09's **Microsoft Defender App Control** policy was restored to **On**.
