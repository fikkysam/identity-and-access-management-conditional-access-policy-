# Lab 10 — Continuous Access Evaluation (CAE): Evidence Pack

This pack contains nine portal screenshots from the controlled SharePoint session-revocation test.

1. `01-admin-session-revocation-success.png` — Entra confirms that Debbie O's sign-in sessions were successfully revoked.
2. `02-existing-sharepoint-session-sign-in-prompt.png` — Existing SharePoint browser session redirects to Microsoft sign-in after the revocation.
3. `03-sign-in-log-is-cae-token-filter.png` — Interactive sign-in log filtered to `Is CAE Token: Yes`.
4. `04-successful-sharepoint-sign-in-cae-yes.png` — Successful SharePoint Online sign-in details show Continuous access evaluation = Yes.
5. `05-failed-sign-in-50133-cae-no.png` — Subsequent failed SharePoint sign-in shows error 50133 (SsoArtifactRevoked) and Continuous access evaluation = No.
6. `06-audit-log-token-valid-from-update.png` — Entra Audit log records `Update StsRefreshTokenValidFrom Timestamp` with Status = success.
7. `07-audit-target-debbie.png` — Audit event target is Debbie O (`debbie@fikayo.onmicrosoft.com`).
8. `08-sharepoint-library-after-reauth.png` — SharePoint Documents library is accessible again after Debbie reauthenticates.
9. `09-lab09-policy-restored-on.png` — Lab 09 Microsoft Defender App Control policy is restored to On.

## Evidence interpretation

The successful SharePoint sign-in was CAE-marked. The administrator session-revocation operation was successful and targeted Debbie. The subsequent SharePoint sign-in failed with 50133 and Entra's additional details describe revoked sessions and a request for new login. However, the failed event itself displayed Continuous access evaluation = No. Therefore, the screenshots support a CAE-capable sign-in followed by an administrator session-revocation/reauthentication flow, but do not independently prove that the failed request itself was processed as a CAE token or that a CAE claims challenge was directly logged.

The Lab 09 Defender App Control policy was confirmed On after the clean-session test.
