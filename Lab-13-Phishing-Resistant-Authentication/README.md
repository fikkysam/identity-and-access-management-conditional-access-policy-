# Lab 13 — Phishing-Resistant Authentication for Privileged Users

## Objective

Require a phishing-resistant authentication method for a narrowly scoped privileged test identity.

## Prerequisites

- Microsoft Entra Conditional Access capability.
- Supported authentication strength.
- Registered FIDO2/passkey or Windows Hello for Business method.
- Dedicated test privileged identity.
- Separate emergency-access account excluded from the policy.
- Non-production tenant.

## Implementation

1. Create or identify a dedicated test privileged identity. Do not experiment with the only Global Administrator account.
2. Register a supported phishing-resistant method for the test identity, such as a FIDO2 security key or Windows Hello for Business.
3. Confirm the authentication strength available in Entra ID and the methods it accepts.
4. Create a Conditional Access policy named `CA-LAB-13-Phishing-Resistant-Privileged`.
5. Target only the dedicated test privileged identity or intended directory-role scope; exclude emergency-access accounts.
6. Target the appropriate administrative resource(s).
7. Under **Grant**, select **Require authentication strength** and choose **Phishing-resistant MFA**.
8. Set the policy to Report-only, save, and test a sign-in with the registered method.
9. Review the sign-in's **Authentication details** and **Conditional Access** tab.
10. Enforce only after a successful controlled test and review of the policy scope/exclusions.

## Validation

- The actual authentication method satisfies the configured phishing-resistant strength.
- The matching sign-in event shows the expected Conditional Access policy result.
- Authentication details identify the method used.
- Excluded emergency-access accounts remain excluded.

## Evidence to capture

- Authentication method registration (no recovery codes or private key data).
- Authentication strength configuration.
- Conditional Access policy scope and emergency-access exclusion.
- Successful sign-in and authentication details.
- Policy evaluation and test notes.

## Current status

**Planned — configuration and controlled phishing-resistant sign-in test not yet performed.**
