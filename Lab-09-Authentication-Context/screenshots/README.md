# Lab 09 — Screenshot Evidence

Upload the PNG files from the Lab 09 evidence ZIP using these exact filenames.

| File | Evidence |
|---|---|
| `01-authentication-context-created-c1.png` | Authentication context Sensitive-Operation created, published, ID C1 |
| `02-conditional-access-targets-authentication-context.png` | Conditional Access policy targets Sensitive-Operation (C1) |
| `03-conditional-access-require-mfa-policy-enabled.png` | MFA grant configured and Conditional Access policy On |
| `04-reports-reader-eligible-assignment-debbie.png` | Debbie O listed in eligible Reports Reader assignments |
| `05-pim-role-settings-require-c1-eight-hours.png` | PIM role activation requires Sensitive-Operation (C1), 8-hour maximum, justification required |
| `06-reports-reader-activation-confirmed.png` | Debbie's Reports Reader active assignment |
| `07-pim-resource-audit-activation-success.png` | PIM audit event: Add member to role completed (PIM activation), success |
| `08-conditional-access-sign-in-frequency-every-time.png` | Conditional Access session control: Sign-in frequency Every time |
| `09-conditional-access-context-matched-policy-success.png` | Debbie and authentication context matched; policy result Success |
| `10-conditional-access-mfa-grant-satisfied-session-enforced.png` | Grant control Require multifactor authentication Satisfied; Session controls Enforced |

## Evidence interpretation

The sign-in event shows the authentication context matched, the policy result was Success, the MFA grant control was Satisfied, and session controls were Enforced.

The user did not observe a separate fresh interactive MFA prompt during activation. Do not caption this evidence as a visible MFA challenge. The logs prove the policy evaluation and that its MFA grant requirement was satisfied for the captured event, not that a new prompt was visibly displayed.

A separate sign-in that did not match the authentication context can correctly show Not applied; do not use that unrelated event as the success evidence.

Never upload passwords, access tokens, client secrets, certificates, private keys, recovery codes, or full token contents.
