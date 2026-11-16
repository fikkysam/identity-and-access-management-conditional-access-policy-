# Lab 09 — Screenshot Evidence

The nine screenshots are stored in the parent lab folder. This index preserves their original filenames.

| # | File | Evidence |
|---:|---|---|
| 1 | [01-entra-policy-overview-on.png](../01-entra-policy-overview-on.png) | Conditional Access policy overview: On, one included user, excluded identity, one resource, and Conditional Access App Control requirement |
| 2 | [02-defender-session-proxy-notification.png](../02-defender-session-proxy-notification.png) | Defender for Cloud Apps proxy notification; routing evidence only |
| 3 | [03-sharepoint-communication-site.png](../03-sharepoint-communication-site.png) | SharePoint Communication site opened in the test session |
| 4 | [04-sharepoint-documents-library.png](../04-sharepoint-documents-library.png) | Documents library used for the test |
| 5 | [05-create-upload-test-file-menu.png](../05-create-upload-test-file-menu.png) | Creating the test text file |
| 6 | [06-test-file-saved.png](../06-test-file-saved.png) | `iam-lab.txt` saved successfully |
| 7 | [07-download-blocked-result.png](../07-download-blocked-result.png) | Browser displays Download blocked for `iam-lab.txt` |
| 8 | [08-defender-session-control-activity.png](../08-defender-session-control-activity.png) | Defender activity identifies the event source as Session control |
| 9 | [09-defender-matched-policy.png](../09-defender-matched-policy.png) | Matched-policy dialog identifies Microsoft Defender App Control, configured in Entra ID |

## Evidence hierarchy

Screenshots 7, 8, and 9 together provide the primary enforcement evidence. Screenshot 2 establishes proxy routing only; do not use it alone to claim that the download was blocked.
