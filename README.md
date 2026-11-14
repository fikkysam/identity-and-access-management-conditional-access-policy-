# Microsoft Entra IAM Engineering Portfolio

A practical portfolio of Microsoft Entra identity security and access-management projects. Each lab records configuration, controlled testing, sign-in evaluation, troubleshooting, and evidence in a non-production tenant.

## Portfolio numbering

This repository contains **13 selected labs**, numbered consecutively from **01 to 13**. The sequence combines the five foundation labs already started with eight selected advanced Conditional Access exercises.

The selected projects are presented in the order they will be completed. The portfolio numbering runs continuously from 01 to 13.

## The 13 selected labs

| Lab | Project | Status |
|---:|---|---|
| 01 | [Block Device Code Authentication](Lab-01-Block-Device-Code/README.md) | Completed — Report-only evaluation verified |
| 02 | [Protect Azure Management](Lab-02-Protect-Azure-Management/README.md) | Completed — policy enabled; successful Conditional Access evaluation and MFA grant verified |
| 03 | [Require Terms of Use Acceptance](Lab-03-Terms-of-Use/README.md) | Completed — acceptance, sign-in and audit evidence verified |
| 04 | [Protect Security Information Registration](Lab-04-Secure-Security-Info-Registration/README.md) | Completed — MFA grant configured, policy On, Authenticator challenge and Conditional Access success documented |
| 05 | [Protect Device Registration and Join](Lab-05-Protect-Device-Registration/README.md) | Partially completed — policy configuration documented; end-to-end device-registration test pending VM capability |
| 06 | [Restrict Access by Operating System](Lab-06-Restrict-Windows-Access/README.md) | Completed — Windows browser block verified in Conditional Access sign-in logs |
| 07 | [Filter Devices by Ownership](Lab-07-Filter-Devices-by-Ownership/README.md) | Completed — non-company/unregistered device browser block verified in Conditional Access sign-in logs |
| 08 | [Authentication Context with PIM](Lab-08-Authentication-Context/README.md) | Completed — PIM Reports Reader activation and C1 Conditional Access evaluation verified |
| 09 | [Conditional Access App Control](Lab-09-Conditional-Access-App-Control/README.md) | Completed — SharePoint download block verified in Defender session-control activity and matched-policy details |
| 10 | [Continuous Access Evaluation (CAE)](Lab-10-Continuous-Access-Evaluation/README.md) | Planned — controlled CAE test and evidence capture |
| 11 | [Workload Identity Conditional Access](Lab-11-Workload-Identity-Conditional-Access/README.md) | Planned — workload identity licensing and supported conditions to be checked |
| 12 | [AI Agent Identity Protection](Lab-12-AI-Agent-Identity-Protection/README.md) | Planned — Agent ID availability, preview status and licensing to be checked |
| 13 | [Phishing-Resistant Authentication for Privileged Users](Lab-13-Phishing-Resistant-Authentication/README.md) | Planned |

## Progress summary

- **Completed:** Labs 01, 02, 03, 04, 06, 07, 08 and 09.
- **Partially completed:** Lab 05. Its Conditional Access policy configuration is documented, but the end-to-end device-registration test and matching sign-in evaluation remain pending.
- **Planned:** Labs 10, 11, 12 and 13.

A lab is not complete until its relevant test and evidence have been captured. Policy creation alone is not sufficient.

## Documentation standard

Each lab should document:
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
- Keep administrator and emergency-access accounts excluded from block policies.
- Prefer Report-only evaluation before enforcement where supported. Any enforcement test must remain narrowly scoped and have a verified administrator exclusion.
- Confirm product licensing and prerequisites before attempting features that depend on Intune, Defender for Cloud Apps, Microsoft Entra Workload ID, Identity Governance, or Agent ID.
- Do not claim a test succeeded unless matching portal state, sign-in/audit logs, or application results support the claim.
- Never publish passwords, temporary device codes, access tokens, secrets, private keys, recovery codes, or unnecessary personal data.

## Learning objective

Demonstrate practical IAM engineering ability across identity protection, Conditional Access, authentication, privileged access, application control, continuous access evaluation, workload identity, agent identity security, phishing-resistant authentication, application federation, hybrid identity, governance, automation, and monitoring.
