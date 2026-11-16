# Lab 06 — Configuration

## Prerequisites

- Non-production Microsoft Entra tenant.
- Dedicated test identity: Don Paul (`don@fikayo.onmicrosoft.com`).
- Separate administrator account with an explicit exclusion from the policy.
- Access to Conditional Access and sign-in logs.

## Policy configuration

| Setting | Configured value |
|---|---|
| Policy name | `restrict windows Access` |
| Users included | Don Paul (`don@fikayo.onmicrosoft.com`) |
| Users excluded | Administrator account |
| Target resources | All resources |
| Device platform | Windows |
| Client apps | Browser |
| Grant | Block access |
| Policy state during test | On |

## Configuration procedure

1. Open **Microsoft Entra admin center → Protection → Conditional Access → Policies**.
2. Create or open the policy named `restrict windows Access`.
3. Under **Users**, include Don Paul and exclude the administrator account.
4. Under **Target resources**, select **All resources**.
5. Under **Conditions → Device platforms**, configure the Windows platform.
6. Under **Conditions → Client apps**, target Browser.
7. Under **Grant**, select **Block access**.
8. Set the policy to **On** for the controlled test.
9. Save the policy and verify its displayed state.

## Scope and operational caution

The policy blocks the selected user's matching Windows browser access across all targeted resources. The administrator exclusion is essential to reduce lockout risk. Keep a separate administrative session available while testing.

The sign-in details for this test identified the browser platform as Windows 10 even though the physical workstation was Windows 11. Document the platform value reported by Entra rather than assuming it will always match the workstation's marketing/version label.

## Evidence

See [screenshots/README.md](screenshots/README.md) for the eight-item configuration and enforcement evidence index.
