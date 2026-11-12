# Lab 07 — Screenshot Evidence

| File | Evidence |
|---|---|
| `01-all-resources-target-selection.png` | All resources selected for the policy |
| `02-device-ownership-filter-rule.png` | Include filtered devices; `device.deviceOwnership -ne "Company"` |
| `03-failed-microsoft-sign-in-error-53003.png` | My Apps denied; Windows 10 and Unregistered shown |
| `04-sign-in-events-failure.png` | Failed interactive sign-in event for Don Paul |
| `05-conditional-access-block-noncompany-policy-failure.png` | Named Lab 07 policy shows Block / Failure; Lab 06 shows Disabled |

The device was an unregistered Windows workstation. Microsoft documents that unregistered device properties evaluate as null and negative device-filter operators can match them. This is a non-company/unknown ownership test, not proof of a positively registered Personal device.

Never publish passwords, access tokens, recovery codes, or private keys.
