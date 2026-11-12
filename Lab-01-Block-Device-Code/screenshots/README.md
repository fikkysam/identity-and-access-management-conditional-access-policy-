# Lab 01 — Block Device Code Authentication: Screenshot Evidence

These are the selected screenshots required to document the Lab 01 configuration and test results. The filenames are numbered sequentially in the order used by this evidence index.

## Evidence index

1. [`01-conditional-access-policy-overview.png`](01-conditional-access-policy-overview.png) — Saved Conditional Access policy overview, including Report-only state and selected configuration.
2. [`02-policy-user-inclusion.png`](02-policy-user-inclusion.png) — Included pilot test user (Debbie O).
3. [`03-policy-administrator-exclusion.png`](03-policy-administrator-exclusion.png) — Excluded administrator account.
4. [`04-device-code-flow-condition.png`](04-device-code-flow-condition.png) — Authentication flows condition with Device code flow selected.
5. [`05-user-sign-in-logs.png`](05-user-sign-in-logs.png) — Sign-in log evidence for the test user and Microsoft Graph Command Line Tools.
6. [`06-policy-evaluation-condition-matches.png`](06-policy-evaluation-condition-matches.png) — Conditional Access evaluation showing the relevant user, resource, and authentication-flow conditions matched.
7. [`07-policy-evaluation-block-grant-control.png`](07-policy-evaluation-block-grant-control.png) — Conditional Access evaluation showing the Block grant control.
8. [`08-report-only-policy-evaluation.png`](08-report-only-policy-evaluation.png) — Report-only result showing Failure; the policy was evaluated but not enforced.

## Interpretation

The policy was configured in **Report-only** mode. A `Report-only: Failure` result means the policy would have blocked the sign-in if enforcement were enabled; it does not mean the Report-only policy blocked the actual sign-in.
