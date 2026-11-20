# Lab 12 — Screenshot Evidence

The following screenshots document the Conditional Access configuration, Jones account passkey registration, and sign-in evaluation.

| # | Filename | Evidence |
|---:|---|---|
| 01 | `01-CA-Policy-User-Group-Inclusion.png` | Included group assignment: `phishing resistant admin` |
| 02 | `02-CA-Policy-Excluded-BreakGlass-Account.png` | Excluded administrative account shown in policy assignment |
| 03 | `03-CA-Grant-Control-Authentication-Strength.png` | Grant controls and authentication-strength configuration |
| 04 | `04-CA-Phishing-Resistant-MFA-Strength-Selected.png` | **Phishing-resistant MFA** selected |
| 05 | `05-CA-Policy-Enabled.png` | Policy state shown as **On** |
| 06 | `06-Jones-Account-MFA-Registration-Prompt.png` | Jones account security-information registration flow |
| 07 | `07-Jones-Authenticator-Number-Matching.png` | Authenticator number-matching prompt during account setup |
| 08 | `08-Jones-Passkey-Creation-Prompt.png` | Browser passkey creation prompt |
| 09 | `09-Jones-Passkey-Created.png` | Microsoft confirms passkey creation for Jones |
| 10 | `10-Jones-My-Apps-Successful-SignIn.png` | Jones account reaches the My Apps dashboard |
| 11 | `11-Jones-SignIn-Conditional-Access-Policy-Result.png` | Conditional Access policy evaluation result |
| 12 | `12-Jones-SignIn-Authentication-Details-Phishing-Resistant.png` | Authentication details showing phishing-resistant requirements satisfied |
| 13 | `13-Jones-Final-Phishing-Resistant-MFA-Test.png` | Final sign-in evidence: first-factor and MFA requirements succeeded |

## Evidence handling

- Screenshots should be committed in this folder using the exact filenames above.
- Do not include passwords, passkey secrets, private keys, recovery codes, or other credential material.
- The sign-in details show **Previously satisfied**. Interpret this as Entra recording the requirement as satisfied, not necessarily as proof of a new passkey prompt during that exact sign-in.
