# Lab 12 — AI Agent Identity Protection

## Objective

Build an identity-security scenario for an AI agent, distinguishing an agent identity, an agent user account, delegated user access, and conventional application/service principal patterns.

## Prerequisites and availability gate

- Non-production Microsoft Entra tenant.
- Check tenant availability for Microsoft Entra Agent ID and any required preview features.
- Required Entra/Agent 365 licensing and administrative roles may apply.
- Dedicated test identities, agent, and non-production resource if hands-on support is available.

**Important:** Do not assume Agent ID is enabled merely because the Entra admin center is available. If the Agents menu or required feature is unavailable, complete the architecture/threat-model and control-design sections and record hands-on validation as blocked by tenant availability.

## Implementation

1. Check **Entra admin center → Agents → Agent identities**. Record whether the feature is available in the tenant.
2. Review Microsoft's current Agent ID documentation and identify whether the scenario uses delegated user access, its own agent identity (app-only), or an agent user account.
3. If the tenant supports Agent ID, create or select a dedicated test agent/blueprint using the documented portal workflow.
4. Assign an accountable owner and sponsor.
5. Inventory the agent's resource access and permissions. Remove unnecessary permissions and document the intended audience/resource.
6. Where supported, assign custom security attributes to classify the agent (for example, `Environment=Lab` and `DataSensitivity=Low`).
7. Create a narrowly scoped Conditional Access policy for the correct agent identity type or blueprint. Start in Report-only and use only controls supported for the selected access pattern.
8. Run a harmless test token/resource-access flow for the agent. Do not connect it to production data.
9. Inspect agent sign-in logs (filter by Agent type / Is Agent where available) and audit logs. Record agent type, resource, policy evaluation, and permissions.
10. Document an incident-response workflow: investigate a suspicious agent, disable the test agent if supported, rotate/revoke its credentials as applicable, and document recovery.

## Validation

- Verify whether the principal is an agent identity, agent user account, or conventional service principal; these are not interchangeable.
- Check agent sign-in and audit events and confirm the relevant Conditional Access target type.
- Record licensing/preview dependencies and any unavailable portal functions.
- Confirm that the agent has only the permissions required for its intended task.

## Evidence to capture

- Agent/blueprint overview, where available.
- Owner/sponsor assignment.
- Permissions inventory and intended resource audience.
- Conditional Access policy and scope.
- Agent sign-in/audit evidence, where available.
- Incident-response runbook and feature-availability notes.

## Current status

**Planned — Agent ID availability, preview status, licensing, and supported policy targets must be checked before implementation.**

A policy for an agent identity does not automatically protect a separate agent user account or delegated user access.
