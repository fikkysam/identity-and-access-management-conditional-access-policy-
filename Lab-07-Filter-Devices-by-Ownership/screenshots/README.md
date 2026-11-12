# Lab 07 — Screenshot Evidence

The numbered evidence set documents the configured device ownership filter and the policy-specific enforcement result.

| File | Evidence |
|---|---|
| `01-all-resources-target-selection.png` | All resources selected for the policy |
| `02-device-ownership-filter-rule.png` | Include filtered devices in policy; rule `device.deviceOwnership -ne "Company"` |
| `03-failed-microsoft-sign-in-error-53003.png` | My Apps sign-in denied; Entra reports Windows 10 and Unregistered |
| `04-sign-in-events-failure.png` | Failed interactive sign-in event for Don Paul |
| `05-conditional-access-block-noncompany-policy-failure.png` | Conditional Access tab shows `Block-NonCompany-Devices`, Block / Failure, and Lab 06 disabled |

**Interpretation:** Microsoft's device-filter documentation says that all device properties are null for unregistered devices, and negative operators can match them. The observed sign-in details show the device was Unregistered. The sign-in's Conditional Access tab identifies this Lab 07 policy as the blocking policy.

The PNG evidence files are prepared separately in the Lab 07 evidence ZIP. Upload them to this folder using the exact filenames above.
