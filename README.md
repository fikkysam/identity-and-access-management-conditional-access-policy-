# Microsoft Entra IAM Engineering Portfolio

A practical portfolio of Microsoft Entra identity security and access-management projects. The work documents configuration, controlled testing, sign-in evaluation, troubleshooting, and security outcomes in a non-production tenant.

## Portfolio structure

This repository is no longer following the original 20-lab workbook. It now follows the **selected project roadmap** in the companion Microsoft Entra IAM Engineering Project Roadmap.

Original exercise numbers are intentionally retained for the eight selected Conditional Access labs so that GitHub stays aligned with the roadmap document.

## Previously completed / started foundation labs

| Exercise | Project | Status |
|---|---|---|
| 01 | [Block Device Code Authentication](Lab-01-Block-Device-Code/README.md) | Completed — Report-only evaluation verified |
| 02 | [Protect Azure Management](Lab-02-Protect-Azure-Management/README.md) | Completed — Policy enabled; successful Conditional Access evaluation and MFA grant verified |
| 03 | [Require Terms of Use Acceptance](Lab-03-Terms-of-Use/README.md) | Completed — acceptance, sign-in and audit evidence verified |
| 04 | [Protect Security Information Registration](Lab-04-Secure-Security-Info-Registration/README.md) | Configuration and validation evidence captured — MFA grant configured, policy On, Authenticator challenge and Conditional Access success documented |
| 05 | [Protect Device Registration and Join](Lab-05-Protect-Device-Registration/README.md) | Configuration completed — end-to-end test pending (VM limitation) |

## Phase 1 — Selected Conditional Access labs

The selected set is **eight labs**, not the original 20. The following exercise numbers are retained from the source workbook for traceability.

| Exercise | Selected project | Status |
|---|---|---|
| 06 | [Restrict Access by Operating System](Lab-06-Restrict-Windows-Access/README.md) | Completed — Windows browser block verified in Conditional Access sign-in logs |
| 07 | [Filter Devices by Ownership](Lab-07-Filter-Devices-by-Ownership/README.md) | Completed — non-company/unregistered device browser block verified in Conditional Access sign-in logs |
| 09 | Authentication Context | Planned |
| 11 | Conditional Access App Control | Planned — licensing and app support to be checked |
| 12 | Continuous Access Evaluation (CAE) | Planned |
| 16 | Workload Identity Conditional Access | Planned — workload identity licensing to be checked |
| 18 | AI Agent Identity Protection | Planned — agent identity availability and licensing to be checked |
| 19 | Phishing-Resistant Authentication for Privileged Users | Planned |

Other exercises from the original 20-lab workbook are not part of the current selected Phase 1 scope.

## Phase 2 — Broader Entra IAM engineering projects

After Phase 1, the portfolio expands beyond Conditional Access into:

1. Privileged Identity Management (PIM)
2. Enterprise application SSO — SAML and OpenID Connect
3. Hybrid identity — Active Directory and Microsoft Entra ID
4. Identity Governance — access packages and access reviews
5. Microsoft Graph and PowerShell IAM automation
6. Identity Protection and risk response
7. Passwordless authentication and authentication methods
8. Identity monitoring, audit logs, and KQL investigation

## Documentation standard

Each project should document:
- Objective and architecture
- Prerequisites, roles, licensing, and limitations
- Exact configuration and scope
- Numbered implementation steps
- Test procedure and observed results
- Sign-in, audit, provisioning, or application evidence
- Troubleshooting and cleanup
- Screenshots stored in a `screenshots/` folder

## Safety and evidence quality

- Use a non-production tenant and dedicated test identities.
- Keep administrator and emergency access accounts excluded from block policies.
- Prefer Report-only evaluation before enforcement where supported. For time-limited exercises, any direct enforcement test must remain narrow and have a verified administrator exclusion.
- Confirm licensing and supporting-product prerequisites before attempting features that depend on Intune, Defender for Cloud Apps, Microsoft Entra Workload ID, Identity Governance, or Agent ID.
- Do not claim a test succeeded unless matching portal state, sign-in/audit logs, or application results support the claim.
- Never publish passwords, temporary device codes, access tokens, secrets, private keys, recovery codes, or unnecessary personal data.

## Learning objective

Demonstrate practical IAM engineering ability across identity protection, Conditional Access, authentication, privileged access, application federation, hybrid identity, governance, automation, and monitoring.
