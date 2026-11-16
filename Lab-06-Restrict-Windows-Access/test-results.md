# Lab 06 — Test Results

## Test objective

Verify that the enabled Conditional Access policy blocks the dedicated test user's browser sign-in when the sign-in is classified as originating from the Windows device platform.

## Test procedure

1. Confirm the policy `restrict windows Access` is On.
2. Confirm Don Paul is included and the administrator account is excluded.
3. From the Windows workstation, attempt browser access as Don Paul.
4. Open the corresponding event in **Microsoft Entra admin center → Monitoring & health → Sign-in logs**.
5. Review the sign-in details and the **Conditional Access** tab.

## Observed results

| Field | Observed value |
|---|---|
| Test identity | Don Paul (`don@fikayo.onmicrosoft.com`) |
| Application | My Apps |
| Device platform reported in sign-in details | Windows 10 |
| Device state | Unregistered |
| Error code | `53003` |
| Sign-in result | Failed |
| Conditional Access policy | `restrict windows Access` |
| Policy grant | Block |
| Policy result | Failure |

The physical workstation used was Windows 11. The sign-in detail page classified the browser platform as Windows 10; this is the value recorded by Entra for the event.

## Result interpretation

**Completed — policy-specific Windows browser block verified.**

Error `53003` is consistent with a Conditional Access-related denial. The stronger attribution is the event's Conditional Access tab, which identifies `restrict windows Access` and displays the Block grant with a Failure result.

## Evidence

See [screenshots/README.md](screenshots/README.md). The key enforcement evidence is:
- `06-failed-sign-in-event.png`
- `07-conditional-access-policy-block-result.png`
- `08-microsoft-error-53003-windows-platform-details.png`

## Limitations and notes

- The event reports Windows 10 even though the physical test workstation was Windows 11.
- The device was reported as Unregistered; this lab's policy condition is the Windows platform and Browser client, not device compliance.
- The result demonstrates the configured policy's effect for this test identity and event. It does not establish behavior for every user, device, client type, or resource.

## Cleanup

If the block is no longer required, turn the policy Off after evidence capture. Keep the administrator exclusion in place while the policy is enabled.
