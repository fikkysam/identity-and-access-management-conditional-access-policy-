# Lab 10 — Test Configuration

## Objective

Exercise a controlled SharePoint session-revocation scenario and inspect the associated Microsoft Entra sign-in and audit evidence for Continuous Access Evaluation (CAE).

## Test environment and flow captured

The evidence pack records:
- A SharePoint browser session for Debbie O (`debbie@fikayo.onmicrosoft.com`).
- An administrator-initiated session-revocation operation.
- A subsequent redirect to Microsoft sign-in from the existing SharePoint session.
- Sign-in log inspection, including the **Is CAE Token** filter and the CAE field on individual events.
- Audit log inspection for the token-valid-from timestamp update.
- Successful access to the SharePoint Documents library after reauthentication.
- Restoration of the Lab 09 Microsoft Defender App Control policy to On.

## Configuration and test sequence represented by evidence

1. Establish an authenticated SharePoint session for the test identity.
2. Use the administrator account to revoke the test identity's sign-in sessions.
3. Return to the existing SharePoint browser session and observe the sign-in redirect.
4. Inspect the sign-in logs and filter for CAE-marked events.
5. Open the successful SharePoint sign-in and inspect its CAE field.
6. Inspect the subsequent failed sign-in and its error details.
7. Review the audit event for `Update StsRefreshTokenValidFrom Timestamp`.
8. Reauthenticate the test user and confirm SharePoint access is restored.
9. Confirm the Lab 09 Defender App Control policy is On after the test.

## Important evidence distinction

The successful SharePoint sign-in is marked **Continuous access evaluation = Yes**. The subsequent failed event shows error `50133` (`SsoArtifactRevoked`) but displays **Continuous access evaluation = No**. The documentation therefore treats the evidence as a CAE-capable sign-in followed by an administrator session-revocation and reauthentication flow. It does not claim that the failed request itself was processed as a CAE token or that a CAE claims challenge was directly logged.

## Evidence

See [screenshots/README.md](screenshots/README.md) for the nine-image evidence index.
