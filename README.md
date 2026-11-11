# Microsoft Entra Conditional Access Labs

A practical portfolio documenting hands-on Microsoft Entra Conditional Access configuration, testing, sign-in evaluation, troubleshooting, and security outcomes.

## Scope

This repository follows a 20-lab Conditional Access workbook. Each lab is documented independently with its objective, prerequisites, configuration, test procedure, observed results, limitations, and evidence.

The work is performed in a non-production Microsoft Entra tenant using a dedicated test identity and a separate administrator account.

## Labs

| Lab | Exercise | Status |
|---|---|---|
| 01 | [Block Device Code Authentication](Lab-01-Block-Device-Code/README.md) | Completed — Report-only evaluation verified |
| 02 | [Protect Azure Management](Lab-02-Protect-Azure-Management/README.md) | Completed — Report-only evaluation verified |
| 03 | [Require Terms of Use Acceptance](Lab-03-Terms-of-Use/README.md) | Completed — acceptance, sign-in and audit evidence verified |
| 04 | [Protect Security Information Registration](Lab-04-Secure-Security-Info-Registration/README.md) | In progress — user scope and user action configured; Grant control and test pending |
| 05 | Protect Device Registration and Join | Planned |
| 06 | Restrict by Operating System | Planned |
| 07 | Filter Devices by Ownership | Planned |
| 08 | Require App Protection Policy for Mobile Access | Planned |
| 09 | Authentication Context | Planned |
| 10 | App-Enforced Restrictions | Planned |
| 11 | Conditional Access App Control | Planned |
| 12 | Continuous Access Evaluation (CAE) | Planned |
| 13 | Persistent Browser Session | Planned |
| 14 | Sign-in Frequency | Planned |
| 15 | Authentication Resilience Settings | Planned |
| 16 | Workload Identity Conditional Access | Planned |
| 17 | Insider-Risk-Based Access | Planned |
| 18 | AI Agent Identity Protection | Planned |
| 19 | Phishing-Resistant Authentication for Privileged Users | Planned |
| 20 | Protect High-Risk Sign-ins and Users | Planned |

## Lab documentation format

Each lab folder can contain:
- `README.md`: objective, security context, and summary
- `configuration.md`: policy configuration and prerequisites
- `test-results.md`: test steps, observed results, and interpretation
- `screenshots/`: evidence captured from the tenant

## Safety and licensing

- Use a non-production tenant and dedicated test identities.
- Keep administrator and emergency access accounts excluded from block policies.
- Use Report-only before enforcement when supported.
- Confirm licensing and supporting-product prerequisites before attempting features that depend on Intune, Defender for Cloud Apps, Purview, or Entra Workload ID.
- Never publish passwords, temporary device codes, access tokens, secrets, or personal data in screenshots.

## Learning objective

Demonstrate the ability to design, configure, test, evaluate, and troubleshoot Conditional Access policies using Microsoft Entra sign-in logs and policy evaluation results.
