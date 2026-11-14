# Lab 09 — Full Evidence Pack

This archive contains nine screenshots, in the order of the lab walkthrough.

| # | Screenshot | What it demonstrates |
|---:|---|---|
| 1 | `01-entra-policy-overview-on.png` | Conditional Access policy overview showing the policy is On, with one included user, an excluded identity, one included resource, and Conditional Access App Control as the access requirement. |
| 2 | `02-defender-session-proxy-notification.png` | SharePoint browser session routed through the Defender for Cloud Apps proxy. The portal notification wording says monitor mode; this image proves routing only, not download enforcement. |
| 3 | `03-sharepoint-communication-site.png` | SharePoint Communication site opened under the test session. |
| 4 | `04-sharepoint-documents-library.png` | Documents library used for the test. |
| 5 | `05-create-upload-test-file-menu.png` | Creating the harmless test text file. |
| 6 | `06-test-file-saved.png` | Test file `iam-lab.txt` saved successfully. |
| 7 | `07-download-blocked-result.png` | Defender for Cloud Apps displayed “Download blocked” for `iam-lab.txt`. |
| 8 | `08-defender-session-control-activity.png` | Redacted activity details showing the download event source was Session control. |
| 9 | `09-defender-matched-policy.png` | Matched policies dialog identifying `Microsoft Defender App Control`, configured in Microsoft Entra ID. |

## Primary validation evidence

The strongest proof of enforcement is the combination of screenshots 7, 8, and 9: the browser block, the Defender session-control activity, and the matched Entra policy. Screenshot 2 documents proxy routing but should not be used alone to claim that downloads were blocked.

The activity-detail screenshot is cropped to avoid exposing the user's full identifier and IP details. The archive is intended for the Lab 09 portfolio evidence folder.
