# Lab 08 — Screenshot Evidence

**Original workbook exercise:** 09 — Authentication Context

| File | Evidence |
|---|---|
| `01-authentication-context-created-c1.png` | Authentication context Sensitive-Operation created and published, ID C1 |
| `02-conditional-access-targets-authentication-context.png` | Conditional Access policy targets Sensitive-Operation (C1) |
| `03-conditional-access-require-mfa-policy-enabled.png` | MFA grant configured and policy On |
| `04-reports-reader-eligible-assignment-debbie.png` | Debbie O listed in eligible Reports Reader assignments |
| `05-pim-role-settings-require-c1-eight-hours.png` | PIM activation requires C1; 8-hour maximum and justification |
| `06-reports-reader-activation-confirmed.png` | Reports Reader shown as activated |
| `07-pim-resource-audit-activation-success.png` | PIM audit: Add member to role completed (PIM activation), successful |
| `08-conditional-access-sign-in-frequency-every-time.png` | Sign-in frequency Every time |
| `09-conditional-access-context-matched-policy-success.png` | Debbie and authentication context matched; policy result Success |
| `10-conditional-access-mfa-grant-satisfied-session-enforced.png` | MFA grant Satisfied and session controls Enforced |

## Evidence interpretation

The sign-in event shows the authentication context matched, the policy result was Success, the MFA grant control was Satisfied, and session controls were Enforced.

Debbie did not observe a separate fresh interactive MFA prompt during activation. Do not caption this evidence as a visible MFA challenge. The logs prove policy evaluation and satisfaction of the MFA grant requirement for the captured event, not that a new prompt was visibly displayed.

A sign-in to an unrelated resource that did not match the authentication context can correctly show Not applied; do not use that event as the success evidence.
