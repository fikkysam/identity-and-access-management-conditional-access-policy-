# Lab 03 — Test Results

## User acceptance test

The test identity opened the Microsoft Entra Terms of Use page.

| Item | Observed result |
|---|---|
| User-facing page | fikayo terms of use |
| Agreement | acceptance use of policy |
| Required action | Read and accept |
| User action | Accept selected |

The captured page showed the instruction to click **Accept** to confirm that the user had read and understood the terms.

## Conditional Access sign-in evaluation

The sign-in event's **Conditional access** tab showed:

| Policy | Grant control | Result |
|---|---|---|
| use of acceptance policy | Use-Agreement | Success |

Other policies were listed in the same sign-in event, including policies marked **Not applied**. The result recorded for this lab is the row corresponding to `use of acceptance policy`.

## Audit log verification

The Terms Of Use audit log showed:

| Field | Observed value |
|---|---|
| Service | Terms Of Use |
| Category | Policy |
| Activity | Accept Terms Of Use |
| Status | Success |
| Initiated by | don paul |

This is the audit event supporting the user's acceptance action.

## Interpretation

The user was presented with the agreement, accepted it, and the matching Conditional Access policy showed **Success** in the sign-in event. The audit log independently recorded **Accept Terms Of Use** with **Success** status.

## Result

**Lab 03: passed.**

Evidence supports:
- Terms of Use document created and displayed.
- User acceptance action completed.
- Conditional Access policy applied to the observed sign-in with a successful Use-Agreement grant result.
- Audit log recorded the acceptance event successfully.

## Limitations

- The captured screenshots do not provide a complete export of the agreement's contents or all policy assignment details.
- The audit event confirms the acceptance action; it does not constitute legal review of the agreement.
- The evidence is limited to the captured test identity, resource and sign-in event.
