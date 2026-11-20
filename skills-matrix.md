# IAM Skills and Tools Matrix

This matrix maps the technical capabilities demonstrated in this repository to the labs and evidence that support them. It is intentionally evidence-based: a tool is listed as **used** only where the lab documentation records its use.

## Skills matrix

| Skill area | Capability demonstrated | Evidence / lab reference |
|---|---|---|
| Microsoft Entra ID | Configure and review Conditional Access policies, assignments, conditions, grant controls, and policy state | Labs 01–10; see each lab's configuration and test documentation |
| Conditional Access evaluation | Interpret user, resource, authentication-flow, device-platform, and device-filter matches; distinguish Report-only from enforcement | Labs 01, 02, 06, 07 |
| Authentication security | Require MFA for Azure management access and security-information registration; evaluate phishing-resistant authentication strength with a registered passkey | Labs 02, 04, and 11 |
| Terms of Use | Configure and validate user acceptance through sign-in and audit evidence | Lab 03 |
| Device-based access control | Apply Windows platform and device-ownership filters to browser access | Labs 06 and 07 |
| Privileged Identity Management | Configure eligible Reports Reader access and validate activation requirements | Lab 08 |
| Authentication context | Create and target authentication context C1 (Sensitive-Operation) from a Conditional Access policy and PIM role activation flow | Lab 08 |
| Defender for Cloud Apps | Validate SharePoint session routing, download restriction, session-control activity, and matched-policy attribution | Lab 09 |
| Continuous Access Evaluation | Analyze CAE-marked sign-in evidence alongside session revocation, reauthentication, and audit records | Lab 10 |
| Identity troubleshooting | Correlate sign-in events, Conditional Access policy details, error codes, audit records, and application behavior | Labs 01–10 and 11, as applicable |
| Evidence-based documentation | Maintain configuration records, test procedures, screenshots, result interpretation, and explicit limitations | Labs 01–10 and 11 |

## Tools and platforms

| Tool / platform | How it is used in this portfolio | Evidence reference |
|---|---|---|
| Microsoft Entra admin center | Configure Conditional Access, authentication contexts, authentication strength, and identity security settings | Labs 01–10 and 11 |
| Microsoft Graph PowerShell SDK | Initiate a delegated device-code authentication test and inspect the resulting Graph context | Lab 01 |
| PowerShell | Run the documented Microsoft Graph PowerShell commands | Lab 01 |
| Microsoft Entra sign-in logs | Inspect sign-in events, Conditional Access evaluation, authentication-flow matches, authentication-strength requirements, and error details | Labs 01–10 and 11, as applicable |
| Microsoft Entra audit logs | Verify Terms of Use acceptance and session-revocation-related audit activity | Labs 03 and 10 |
| Microsoft Entra Privileged Identity Management | Configure and test eligible Reports Reader role activation | Lab 08 |
| Microsoft Authenticator | Observe the MFA challenge during security-information registration and test-account setup | Labs 04 and 11 |
| Microsoft Defender for Cloud Apps | Inspect session-control activity and matched-policy details for a SharePoint download restriction | Lab 09 |
| SharePoint Online | Provide the test site, Documents library, browser session, and test file for session-control and CAE exercises | Labs 09 and 10 |
| Azure Resource Manager | Serve as the target resource for the Azure management Conditional Access exercise | Lab 02 |
