# Lab 12 — Configuration

## 1. Test identity and scope

| Setting | Observed configuration |
|---|---|
| Test account | `jones@fikayo.onmicrosoft.com` |
| Included group | `phishing resistant admin` |
| Excluded account | Global Administrator operator account (shown in the policy's excluded users) |
| Conditional Access policy | `phishing resistant MFA` |
| Authentication strength | **Phishing-resistant MFA** |
| Policy state | **On** in the captured policy overview |
| Test credential | Passkey saved in Google Password Manager |

The account used for this test was **Jones**, not `labadmin`. Earlier screenshots and tests involving other accounts are not attributed to this Lab 12 validation.

## 2. Conditional Access policy

The policy was configured in Microsoft Entra admin center:

1. Open **Protection → Conditional Access → Policies**.
2. Create a policy named `phishing resistant MFA`.
3. Under **Users and groups → Include**, select the `phishing resistant admin` group.
4. Under **Exclude**, select the Global Administrator operator account used to administer the lab.
5. Under **Grant**, select **Grant access** and **Require authentication strength**.
6. Select **Phishing-resistant MFA** from the authentication-strength list.
7. Save the policy. The captured policy overview later showed the policy state as **On**.

The portal displayed a warning that **Require authentication strength** cannot be combined with the separate **Require multifactor authentication** checkbox. The policy therefore uses the authentication-strength control rather than selecting both controls.

> Review the complete target-resource configuration in the tenant before reproducing this policy. The screenshots retained for this lab do not provide a sufficiently clear, complete record of the final target-resource selection to assert a specific resource scope here.

## 3. Passkey registration

1. Sign in as `jones@fikayo.onmicrosoft.com`.
2. Open [Security info](https://mysignins.microsoft.com/security-info).
3. Select **Add sign-in method**.
4. Choose **Passkey**.
5. Complete the browser's passkey creation flow.
6. Save the passkey in Google Password Manager and finish the Microsoft registration flow.

The browser confirmed **Passkey created** for the Jones account. Google Password Manager stores the passkey credential; the password manager PIN is used to unlock or authorize use of the stored credential.

## 4. Authentication method distinction

A passkey is based on the FIDO2/WebAuthn standard. It is phishing-resistant because authentication is cryptographically bound to the relying party (the legitimate website origin). A password manager PIN is not the Microsoft account password; it unlocks the local or synced passkey credential.

A passkey saved in Google Password Manager is a passkey credential. It should not be described as a physical FIDO2 security key.

## 5. Safety notes

- Use a dedicated test account and a narrowly scoped group.
- Keep a separate, secure administrative recovery path.
- Do not include the only Global Administrator account in a policy that could prevent administrative access.
- Keep secrets, recovery codes, and credential material out of screenshots and source control.
