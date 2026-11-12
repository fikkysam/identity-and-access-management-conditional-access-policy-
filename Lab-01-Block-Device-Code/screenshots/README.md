# Lab 01 — Block Device Code: Screenshot Evidence

This folder contains the evidence screenshots for the **Block Device Code Conditional Access** lab.

## Required evidence

| Filename | Evidence |
|---|---|
| `01-conditional-access-policy-overview.png` | Saved policy overview |
| `02-policy-user-inclusion.png` | Test user included in the policy |
| `03-policy-administrator-exclusion.png` | Administrator excluded from the policy |
| `04-device-code-flow-condition.png` | Device Code Flow condition selected |
| `05-user-sign-in-logs.png` | Sign-in logs for the test |
| `06-policy-condition-matches.png` | User, resource, and authentication flow matched |
| `07-block-grant-control.png` | Block grant control evaluated |
| `08-report-only-failure-result.png` | Report-only failure result |

Upload the eight PNG files above into this folder. The policy was configured in **Report-only** mode; a Report-only failure means the policy would have blocked the sign-in if enforcement were enabled, not that the policy actively blocked the sign-in.

Review screenshots before publishing. Remove temporary device codes, tokens, session identifiers, and other secrets.
