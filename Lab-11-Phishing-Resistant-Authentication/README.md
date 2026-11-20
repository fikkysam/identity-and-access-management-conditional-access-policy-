# Lab 11 — Phishing-Resistant Authentication for Privileged Users

<badge>Completed — controlled test</badge>

A dedicated test account registered a passkey, and a subsequent successful sign-in was evaluated against the Conditional Access policy using the **Phishing-resistant MFA** authentication strength. See the evidence limitations in [test-results.md](test-results.md).

## Objective

Require a phishing-resistant authentication method for a narrowly scoped privileged test identity using Microsoft Entra Conditional Access authentication strength.

## Scenario

A dedicated test account, `jones@fikayo.onmicrosoft.com`, was used to validate a phishing-resistant authentication flow. The Conditional Access policy was named **phishing resistant MFA** and targeted the **phishing resistant admin** group. The operator's Global Administrator account was excluded from the user assignment during policy configuration.

The test used a passkey saved in Google Password Manager. This is a passkey-based FIDO2/WebAuthn sign-in credential; it is not a physical USB security key.

## Lab structure

| File / folder | Purpose |
|---|---|
| [configuration.md](configuration.md) | Policy scope, authentication strength, and passkey registration |
| [test-results.md](test-results.md) | Controlled test, observed sign-in evaluation, and limitations |
| [screenshots/README.md](screenshots/README.md) | Evidence index for the 13 screenshots |

## Key outcome

The sign-in log showed the **phishing resistant MFA** Conditional Access policy with a **Success** result. Authentication details showed successful first-factor and MFA requirement rows, each with the phishing-resistant requirement. The details displayed **Previously satisfied**, so the evidence supports that Entra considered the requirements satisfied for the sign-in.

## Important limitations

- The Authentication details view does not expose the specific passkey provider or credential identifier in the captured rows. The separate registration evidence shows that a passkey was created for the Jones test account.
- The captured event shows the requirements as **Previously satisfied**; it does not prove that a fresh passkey prompt occurred during that exact sign-in.
- This is a controlled lab validation, not a production rollout or proof of phishing-resistant authentication for every privileged identity.
- Keep the policy scoped to the intended test group and retain a safe administrative exclusion. Do not enable a broad policy without reviewing its complete resource scope and exclusions.

## Related portfolio links

- [Portfolio overview](../README.md)
- [IAM skills and tools matrix](../skills-matrix.md)
