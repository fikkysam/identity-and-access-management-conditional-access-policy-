# Lab 11 — Workload Identity Conditional Access

**Original workbook exercise:** 16 — Workload identity Conditional Access

## Objective

Protect service principals/workload identities using workload identity Conditional Access rather than user-based Conditional Access policies.

## Prerequisites and licensing gate

- Microsoft Entra Workload ID licensing as applicable to the feature and scenario.
- Dedicated non-production app registration/service principal.
- Test resource and least-privilege permissions.
- Appropriate administrator role.
- Certificate or federated credential preferred; avoid committing long-lived client secrets.

## Implementation

1. Confirm workload identity Conditional Access availability and licensing in the tenant.
2. Create a non-production app registration dedicated to this lab; record its application ID and service principal object ID.
3. Grant only the minimum API/application permissions needed for the test. Obtain admin consent only where required.
4. Configure certificate-based or federated authentication where supported.
5. Create a Conditional Access policy for **Workload identities** and select the dedicated service principal under workload identity assignments.
6. Configure only a condition and grant control supported for workload identity policies in this tenant, such as a named-location restriction or block scenario.
7. Exclude unrelated production workloads; use Report-only where the workload identity policy experience supports it.
8. Request a token and access only the lab resource using the dedicated service principal.
9. Inspect service principal sign-in logs and the Conditional Access policy evaluation.
10. Verify the app still has only the permissions required for the test.

## Validation

- The correct service principal is targeted, not the human user who created it.
- Workload identity sign-in logs show the test activity.
- Conditional Access evaluation matches the selected workload identity policy and supported condition.
- App permissions remain least-privileged.

## Evidence to capture

- App registration and service principal details (IDs only; no credential material).
- Permission inventory and rationale.
- Workload identity Conditional Access policy.
- Token/access test result.
- Service principal sign-in logs and policy evaluation.

## Current status

**Planned — workload identity licensing, availability, and supported conditions must be confirmed before implementation.**

Workload identity Conditional Access is distinct from user Conditional Access. Do not test with production service principals.
