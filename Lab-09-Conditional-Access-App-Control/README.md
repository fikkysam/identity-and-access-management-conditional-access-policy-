# Lab 09 — Conditional Access App Control

**Original workbook exercise:** 11 — Conditional Access App Control

## Objective

Route supported cloud-app sessions through Microsoft Defender for Cloud Apps for session monitoring or control.

## Prerequisites and licensing gate

- Microsoft Entra Conditional Access capability.
- Microsoft Defender for Cloud Apps entitlement and onboarding.
- A supported cloud application that supports session control.
- Dedicated test user and separate administrator exclusion.
- Non-production test data.

**Important:** Entra ID P2 alone does not establish that Defender for Cloud Apps is licensed and onboarded. Confirm the Defender for Cloud Apps entitlement and target-app support before proceeding.

## Implementation

1. Confirm Defender for Cloud Apps licensing and service availability in the tenant.
2. Verify that the target cloud application is onboarded and supports session control.
3. In Defender for Cloud Apps, configure the relevant cloud-app connection/session-control integration using Microsoft's current onboarding guidance.
4. In Microsoft Entra admin center, create a Conditional Access policy named `CA-LAB-09-Defender-Session-Control`.
5. Include only the dedicated test user; exclude administrator and emergency-access identities.
6. Target the onboarded, supported cloud application.
7. Under **Session**, select **Use Conditional Access App Control**.
8. Choose **Monitor only** for the initial test, if available and appropriate.
9. Keep the policy in Report-only until the integration and scope have been checked.
10. Sign in to the app using the test identity and verify whether the session is routed through Defender for Cloud Apps.
11. Inspect Defender for Cloud Apps activity/session logs and Entra sign-in evaluation.
12. Only after a successful monitor-only test, consider a narrowly scoped session policy such as controlling downloads of a harmless test file.

## Validation

- The intended test user and application match the Conditional Access policy.
- The sign-in event records the expected policy evaluation.
- The session is routed through Defender for Cloud Apps.
- Defender for Cloud Apps records the session activity.
- Any additional session policy is tested with non-sensitive data.

## Evidence to capture

- Defender for Cloud Apps licensing/onboarding and supported app configuration.
- Conditional Access policy scope and session control.
- Sign-in log and Conditional Access evaluation.
- Defender for Cloud Apps session activity.
- Session policy and controlled test result, if configured.

## Current status

**Planned — licensing and application support must be confirmed before implementation.** Do not mark this lab complete merely because the Conditional Access policy can be saved.
