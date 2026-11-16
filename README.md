# Microsoft Entra IAM Engineering Portfolio

A hands-on identity and access management (IAM) engineering portfolio focused on **Microsoft Entra ID, Conditional Access, authentication security, privileged access, and identity governance**.

This repository documents practical work performed in a non-production Microsoft Entra tenant. Each lab is intended to show more than policy creation: it records the objective, configuration, scope, controlled test, observed outcome, and supporting evidence.

> **Portfolio principle:** configuration is not proof of enforcement. Completion claims are tied to the test results and evidence documented for each lab.

## Portfolio at a glance

| Measure | Current status |
|---|---:|
| Selected labs | 13 |
| Completed | 9 |
| Partially completed | 1 |
| Planned | 3 |

The portfolio is organized as a progressive sequence, from foundational Conditional Access controls to advanced identity-security scenarios.

## Lab catalogue

| Lab | Project | Status |
|---:|---|---|
| 01 | [Block Device Code Authentication](Lab-01-Block-Device-Code/README.md) | **Completed** — Report-only evaluation verified; the policy was not represented as an enforced block |
| 02 | [Protect Azure Management](Lab-02-Protect-Azure-Management/README.md) | **Completed** — policy enabled; successful Conditional Access evaluation and MFA grant verified |
| 03 | [Require Terms of Use Acceptance](Lab-03-Terms-of-Use/README.md) | **Completed** — acceptance, sign-in, and audit evidence verified |
| 04 | [Protect Security Information Registration](Lab-04-Secure-Security-Info-Registration/README.md) | **Completed** — MFA grant configured, policy On, Authenticator challenge, and Conditional Access success documented |
| 05 | [Protect Device Registration and Join](Lab-05-Protect-Device-Registration/README.md) | **Partially completed** — policy configuration documented; end-to-end device-registration test pending VM capability |
| 06 | [Restrict Access by Operating System](Lab-06-Restrict-Windows-Access/README.md) | **Completed** — Windows browser block verified in Conditional Access sign-in logs |
| 07 | [Filter Devices by Ownership](Lab-07-Filter-Devices-by-Ownership/README.md) | **Completed** — non-company/unregistered device browser block verified in Conditional Access sign-in logs |
| 08 | [Authentication Context with PIM](Lab-08-Authentication-Context/README.md) | **Completed** — PIM Reports Reader activation and C1 Conditional Access evaluation verified |
| 09 | [Conditional Access App Control](Lab-09-Conditional-Access-App-Control/README.md) | **Completed** — SharePoint download block verified in Defender session-control activity and matched-policy details |
| 10 | [Continuous Access Evaluation (CAE)](Lab-10-Continuous-Access-Evaluation/README.md) | **Completed** — CAE-capable SharePoint sign-in, administrator session revocation, reauthentication, and audit evidence verified |
| 11 | [Workload Identity Conditional Access](Lab-11-Workload-Identity-Conditional-Access/README.md) | **Planned** — workload identity licensing and supported conditions to be checked |
| 12 | [AI Agent Identity Protection](Lab-12-AI-Agent-Identity-Protection/README.md) | **Planned** — Agent ID availability, preview status, and licensing to be checked |
| 13 | [Phishing-Resistant Authentication for Privileged Users](Lab-13-Phishing-Resistant-Authentication/README.md) | **Planned** |

### Progress

- **Completed:** Labs 01, 02, 03, 04, 06, 07, 08, 09, and 10.
- **Partially completed:** Lab 05. The policy configuration is documented, but the end-to-end device-registration test and matching sign-in evaluation remain pending.
- **Planned:** Labs 11, 12, and 13.

A lab is not marked complete solely because a policy was created. Its status reflects the test and evidence currently documented in the repository.

## Technical areas demonstrated

The completed labs provide practical evidence across these areas:

- **Conditional Access policy engineering:** policy scope, assignments, conditions, grant controls, session controls, and Report-only evaluation.
- **Authentication security:** MFA requirements, security-information registration, and Terms of Use acceptance.
- **Device-based access control:** operating-system restrictions and device ownership filtering.
- **Privileged access:** Privileged Identity Management (PIM) activation combined with Conditional Access authentication context.
- **Application session protection:** Microsoft Defender for Cloud Apps session control and SharePoint download restrictions.
- **Session lifecycle security:** Continuous Access Evaluation concepts, administrator session revocation, and reauthentication analysis.
- **Identity troubleshooting and evidence:** sign-in logs, policy evaluation details, audit evidence, application behavior, and documented test limitations.

The planned labs extend the portfolio into workload identities, AI agent identity protection, and phishing-resistant authentication for privileged users. These are future objectives, not claims of completed implementation.

## How each lab is documented

Where the lab structure supports it, documentation is organized into:

| File | Purpose |
|---|---|
| `README.md` | Lab overview, objective, scope, and navigation |
| `configuration.md` | Prerequisites, policy settings, assignments, and implementation details |
| `test-results.md` | Test procedure, observed outcome, evidence interpretation, and limitations |
| `screenshots/README.md` | Screenshot index explaining what each item demonstrates |

Some earlier labs retain a simpler documentation layout. The repository is being progressively standardized without changing the underlying test results or overstating what the evidence proves.

## Evidence and testing approach

Each lab uses a controlled workflow:

1. **Define the objective** — identify the identity-security risk or access-control requirement.
2. **Check prerequisites** — confirm licensing, roles, tenant capabilities, and any dependent services.
3. **Configure narrowly** — scope policies to dedicated test identities and intended resources.
4. **Protect administrative access** — exclude administrator or emergency-access accounts from policies that could lock them out.
5. **Test deliberately** — use a defined user, application, device, or authentication flow.
6. **Inspect the result** — review Conditional Access evaluation, sign-in logs, audit records, and application behavior as applicable.
7. **Record limitations** — distinguish what was directly observed from what the evidence does not establish.

### Safety and evidence quality

- All exercises are intended for a **non-production tenant**.
- Use dedicated test identities and narrowly scoped policies.
- Prefer Report-only evaluation before enforcement where supported.
- Clearly distinguish a Report-only result from an enforced access block.
- Verify the relevant sign-in, audit, or application evidence before claiming a control worked.
- Check licensing and prerequisites for features that depend on services such as Intune, Defender for Cloud Apps, Microsoft Entra Workload ID, Identity Governance, or Agent ID.
- Do not publish passwords, temporary device codes, access tokens, secrets, private keys, recovery codes, or unnecessary personal information.

## Repository roadmap

The next development priorities are:

1. Complete the end-to-end validation for Lab 05 when the required VM/device capability is available.
2. Continue standardizing documentation and screenshot indexes across the existing labs.
3. Implement and validate the planned advanced identity-security labs (11–13), subject to licensing and feature availability.

## Learning objective

Build and demonstrate practical IAM engineering capability through repeatable configuration, controlled testing, troubleshooting, and evidence-based documentation in Microsoft Entra ID.

The portfolio is designed to show not only how identity controls are configured, but also how their behavior is validated, interpreted, and documented.
