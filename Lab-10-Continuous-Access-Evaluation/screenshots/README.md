# Lab 10 — Screenshot Evidence

The nine screenshots are stored in the parent lab folder. This index preserves their original filenames.

| # | File | Evidence |
|---:|---|---|
| 1 | [01-admin-session-revocation-success.png](../01-admin-session-revocation-success.png) | Entra confirms Debbie O's sign-in sessions were successfully revoked |
| 2 | [02-existing-sharepoint-session-sign-in-prompt.png](../02-existing-sharepoint-session-sign-in-prompt.png) | Existing SharePoint session redirects to Microsoft sign-in |
| 3 | [03-sign-in-log-is-cae-token-filter.png](../03-sign-in-log-is-cae-token-filter.png) | Interactive sign-in log filtered to Is CAE Token: Yes |
| 4 | [04-successful-sharepoint-sign-in-cae-yes.png](../04-successful-sharepoint-sign-in-cae-yes.png) | Successful SharePoint Online sign-in shows CAE = Yes |
| 5 | [05-failed-sign-in-50133-cae-no.png](../05-failed-sign-in-50133-cae-no.png) | Subsequent failed sign-in shows 50133 (SsoArtifactRevoked) and CAE = No |
| 6 | [06-audit-log-token-valid-from-update.png](../06-audit-log-token-valid-from-update.png) | Audit log records Update StsRefreshTokenValidFrom Timestamp, Status = success |
| 7 | [07-audit-target-debbie.png](../07-audit-target-debbie.png) | Audit event target is Debbie O |
| 8 | [08-sharepoint-library-after-reauth.png](../08-sharepoint-library-after-reauth.png) | SharePoint Documents library accessible after reauthentication |
| 9 | [09-lab09-policy-restored-on.png](../09-lab09-policy-restored-on.png) | Lab 09 Microsoft Defender App Control policy restored to On |

## Evidence interpretation

The successful SharePoint sign-in is marked CAE = Yes. The later failed event is marked CAE = No; preserve this distinction. The screenshots support the session-revocation and reauthentication flow but do not independently show that the failed request was a CAE token or that a CAE claims challenge was directly logged.
