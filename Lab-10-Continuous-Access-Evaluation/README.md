# Lab 10 — Continuous Access Evaluation (CAE)

## Objective

Observe how a CAE-capable resource and client respond to supported critical events and changes in access conditions during an active user session.

## Prerequisites

- Dedicated test identity.
- CAE-capable resource and client, such as a supported Microsoft 365 workload/client.
- Separate administrator identity for controlled account/session operations.
- Non-production test session.
- Entra sign-in and audit log access.

## Technical note

CAE is not a universal instant-logout feature and is not simply enabled by creating a separate Conditional Access policy. The resource and client must support CAE, and the response depends on the event and workload.

## Implementation

1. Review Microsoft's current CAE support information for the resource and client you intend to test.
2. Select a supported resource/client and record names, versions, and applicable support limitations.
3. Sign in as the dedicated test user and confirm the session is established.
4. Record the initial sign-in event, resource, client, device, time, and correlation/request identifiers.
5. From the separate administrator session, perform a safe critical event supported by the test scenario, following Microsoft's documented test method.
6. Observe whether the active client/resource requests a new token, challenges the user, or restricts/denies the session.
7. Check Entra sign-in logs and audit logs for the initiating event and any subsequent authentication.
8. Record the observed response and elapsed time. Do not assume an immediate response if the resource/client does not support the scenario.
9. Where practical, compare with a client/resource that does not support the same CAE behavior and document the difference.

## Validation

- The test resource and client are supported for the scenario.
- The initiating event is recorded in the audit trail.
- The active session's observed response is documented.
- The result is not generalized beyond the tested resource, client, and event.
- CAE behavior is distinguished from ordinary token expiry or a new sign-in.

## Evidence to capture

- Support-matrix reference and resource/client details.
- Initial sign-in event.
- Audit event for the critical action.
- Observed client/resource response and timeline.
- Follow-up sign-in or authentication details, where generated.

## Current status

**Planned — controlled CAE test and evidence capture not yet performed.**
