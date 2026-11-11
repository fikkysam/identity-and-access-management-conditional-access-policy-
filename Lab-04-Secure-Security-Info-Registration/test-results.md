# Lab 04 — Test Results

## Current test status

**Not yet tested — policy configuration is incomplete.**

The available screenshots document the policy creation and assignment scope, but do not show a configured Grant control or a completed policy.

## Configuration evidence

| Item | Observed result |
|---|---|
| Policy name | Require MFA for Security Info Registration |
| Included user | don paul |
| Excluded administrator | Oluwafikayo Oyedokun |
| Target user action | Register security information |
| Grant control | 0 controls selected |
| Policy state | Report-only on the creation screen |

## Required validation procedure

After configuring the Grant control and creating the policy:

1. Sign in as the dedicated test identity.
2. Open the security information registration experience.
3. Perform the registration action in a controlled test.
4. Locate the corresponding event in **Microsoft Entra admin center → Monitoring & health → Sign-in logs**.
5. Inspect the **Conditional Access** and, where available, **Report-only** evaluation details.
6. Confirm that the policy, user-action target and MFA/authentication-strength requirement are evaluated as expected.
7. Capture the event and record the actual result.

## Expected result

The policy should evaluate for the Register security information user action and indicate whether the MFA/authentication-strength grant requirement would be satisfied or would require user action.

Do not mark the test as passed based only on the policy creation screen. Report-only evaluates policy impact and does not enforce the grant control.

## Completion checklist

- [x] Dedicated test user included.
- [x] Administrator account excluded.
- [x] Register security information user action selected.
- [ ] Grant access configured.
- [ ] MFA or appropriate authentication strength selected.
- [ ] Policy created in Report-only.
- [ ] Test-user registration attempt completed.
- [ ] Matching sign-in event reviewed.
- [ ] Conditional Access evaluation captured.
- [ ] Final evidence screenshots uploaded.

## Result

**Lab 04 remains in progress.** No successful policy evaluation or registration test is claimed at this stage.
