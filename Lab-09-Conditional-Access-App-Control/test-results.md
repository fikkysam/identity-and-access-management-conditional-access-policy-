# Lab 09 — Test Results

## Test objective

Verify that a SharePoint browser session routed through Microsoft Defender for Cloud Apps is subject to a download restriction, and corroborate the result with Defender session-control activity and matched-policy details.

## Test procedure represented in the evidence

1. Open the scoped SharePoint Communication site.
2. Navigate to the Documents library.
3. Create and save `iam-lab.txt`.
4. Attempt to download the file from the browser session.
5. Review the browser result.
6. Review the corresponding Defender for Cloud Apps session-control activity.
7. Inspect the matched-policy details.

## Observed results

| Validation | Evidence / observation |
|---|---|
| Conditional Access policy | Policy overview shows state On |
| Proxy routing | Defender session proxy notification displayed |
| SharePoint test location | Communication site and Documents library opened |
| Test file | `iam-lab.txt` saved successfully |
| Download attempt | Browser displayed **Download blocked** |
| Session activity | Defender activity details identify the source as **Session control** |
| Policy attribution | Matched policies dialog identifies **Microsoft Defender App Control**, configured in Microsoft Entra ID |

## Result interpretation

**Completed — SharePoint download block verified.**

The strongest validation is the combination of:
1. The browser's **Download blocked** result.
2. Defender's session-control activity for the download event.
3. The matched-policy dialog identifying Microsoft Defender App Control.

The proxy notification demonstrates routing only. Its monitor-mode wording means it must not be presented as standalone proof of enforcement.

## Evidence

See [screenshots/README.md](screenshots/README.md). Screenshots 7–9 provide the primary enforcement and attribution evidence.

## Scope and limitations

- The evidence demonstrates the observed SharePoint test-file download restriction in the captured session.
- It does not establish that every file type, SharePoint site, user, browser, or download path is blocked.
- The evidence pack does not preserve all granular policy wizard settings; configuration statements should remain limited to what the screenshots support.
- The activity-detail screenshot is cropped to avoid exposing the user's full identifier and IP details.

## Cleanup

The evidence pack does not record a separate cleanup operation. Before reusing the tenant, review the Conditional Access policy and Defender session policy and decide whether they should remain enabled.
