# Lab 11 — Test Results

## Test objective

Verify that the Jones test account can complete a sign-in after registering a passkey and that Microsoft Entra evaluates the sign-in against the **Phishing-resistant MFA** authentication strength.

## Test record

| Item | Result |
|---|---|
| Test identity | `jones@fikayo.onmicrosoft.com` |
| Passkey registration | **Successful** — Microsoft displayed **Passkey created** |
| Credential storage | Google Password Manager |
| Conditional Access policy | `phishing resistant MFA` |
| Policy result in sign-in details | **Success** |
| Authentication-strength requirement | **Phishing-resistant** |
| Authentication detail rows | First-factor requirement and MFA requirement both show **Succeeded: Yes** |
| Result detail | **Previously satisfied** for both rows in the captured event |

## Procedure and observed results

1. Registered a passkey for the Jones test account through the Microsoft Security info page.
2. Confirmed the Microsoft page displayed **Passkey created**.
3. Completed a sign-in as the Jones account.
4. Opened the corresponding event in **Microsoft Entra → Monitoring & health → Sign-in logs**.
5. Reviewed the **Conditional access** tab. The policy named `phishing resistant MFA` showed **Success**.
6. Reviewed **Authentication details**. The captured event showed two successful requirement rows: first-factor requirement and MFA requirement. Both displayed the phishing-resistant requirement.

## Conclusion

**The controlled test passed at the Conditional Access evaluation level.** The evidence shows a passkey was registered for the Jones account and a successful sign-in was evaluated with the phishing-resistant authentication-strength requirement satisfied.

## Evidence limitations

- The Authentication details screenshot shows **Previously satisfied**, not a fresh passkey challenge in that exact sign-in transaction.
- The captured Authentication details rows do not identify the specific credential provider or explicitly label the method as Google Password Manager. The separate passkey-registration screenshot establishes that a passkey was created for Jones.
- The sign-in evidence therefore supports successful evaluation of the phishing-resistant authentication strength, but does not independently show the exact credential ceremony or prove which device/provider supplied the assertion.
- The screenshots in this lab do not clearly preserve the final target-resource selection. Verify that scope in the tenant before treating this as a reusable production policy.
- This test validates one account and one controlled scenario; it is not evidence of tenant-wide deployment.

## Evidence

See [screenshots/README.md](screenshots/README.md) for the screenshot-by-screenshot index.
