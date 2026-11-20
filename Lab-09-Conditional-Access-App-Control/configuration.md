# Lab 09 — Configuration

## Objective

Configure Conditional Access App Control for a SharePoint browser session and validate a download restriction through Microsoft Defender for Cloud Apps session control.

## Configuration evidence available

The retained screenshot set documents these observed configuration and setup details:

| Area | Evidence-supported observation |
|---|---|
| Conditional Access policy | Policy overview shows the policy On |
| User scope | One included user and an excluded identity are visible |
| Resource scope | One included resource is visible |
| Access requirement | Conditional Access App Control |
| Session routing | SharePoint browser session displays the Defender for Cloud Apps proxy notification |
| Test resource | SharePoint Communication site and Documents library |
| Test file | `iam-lab.txt` |

The screenshot showing the proxy notification uses monitor-mode wording. It is evidence that the session was routed through the proxy, not proof by itself that a download was blocked.

## Implementation flow represented by the evidence

1. Configure and enable the Conditional Access policy with Conditional Access App Control as the access requirement.
2. Open the SharePoint site and Documents library in the scoped browser session.
3. Create and save the harmless test file `iam-lab.txt`.
4. Attempt to download the test file.
5. Review the browser response and Defender for Cloud Apps session-control activity.
6. Inspect the matched-policy details to confirm the associated policy.

## Evidence

See [screenshots/README.md](screenshots/README.md) for the nine-image index and the distinction between routing evidence and enforcement evidence.
