# Lab 10 — Test Results

## Test objective

Validate the administrator session-revocation and reauthentication flow for an existing SharePoint session, then correlate the observed behavior with Entra sign-in and audit records.

## Test procedure

1. Establish a SharePoint session as Debbie O.
2. Revoke Debbie's sign-in sessions from the administrator context.
3. Return to the existing SharePoint session.
4. Observe the redirect to Microsoft sign-in.
5. Review the relevant sign-in events, including the CAE token filter and individual event details.
6. Review the audit log for the token-valid-from timestamp update.
7. Reauthenticate Debbie and verify that SharePoint access is restored.

## Observed results

| Evidence | Observed result |
|---|---|
| Session revocation | Administrator session-revocation operation succeeded |
| Existing SharePoint session | Redirected to Microsoft sign-in |
| CAE token filter | Sign-in log filtered to `Is CAE Token: Yes` |
| Successful SharePoint sign-in | Continuous access evaluation = Yes |
| Subsequent failed sign-in | Error `50133` (`SsoArtifactRevoked`) |
| CAE field on failed event | Continuous access evaluation = No |
| Audit log | `Update StsRefreshTokenValidFrom Timestamp`, Status = Success |
| Audit target | Debbie O (`debbie@fikayo.onmicrosoft.com`) |
| After reauthentication | SharePoint Documents library accessible again |
| Lab 09 policy state | Microsoft Defender App Control policy restored to On |

## Result interpretation

**Completed — CAE-capable SharePoint sign-in, administrator session revocation, reauthentication, and audit evidence captured.**

The successful SharePoint sign-in is explicitly marked CAE = Yes. The administrator's session-revocation operation succeeded and the audit event targets Debbie. The existing SharePoint session then required sign-in, and access was restored after reauthentication.

## Evidence limitation

The subsequent failed SharePoint event shows error `50133` (`SsoArtifactRevoked`) and the details describe revoked sessions and a request for a new login. However, that failed event itself displays CAE = No.

Accordingly, this evidence supports a CAE-capable sign-in followed by an administrator session-revocation/reauthentication flow. It does **not** independently prove that the failed request itself was processed as a CAE token, nor does it show a CAE claims challenge directly logged.

## Evidence

See [screenshots/README.md](screenshots/README.md). Screenshots 1, 2, 4, 5, 6, 7, and 8 provide the main sequence and corroborating records.

## Cleanup and operational notes

The final screenshot confirms that the Lab 09 Microsoft Defender App Control policy was restored to On after the clean-session test. Review the test policies and session state before using the tenant for other exercises. Do not publish tokens, secrets, or recovery codes.
