# Lab 01 — Block Device Code Authentication

## Objective

Configure a Microsoft Entra Conditional Access policy to identify and block sign-ins that use the device-code authentication flow for a dedicated pilot user.

## Security context

Device-code authentication is a legitimate sign-in flow used by command-line tools and devices that may not have a convenient browser. It can also be abused in device-code phishing scenarios, where a user is tricked into completing an authentication request initiated by someone else.

This lab demonstrates how Conditional Access can target the device-code authentication flow.

## Lab environment

- Microsoft Entra ID non-production tenant
- Separate administrator account used to configure the policy and review sign-in logs
- Dedicated test account: Debbie O
- Microsoft Graph PowerShell Authentication module
- Microsoft Graph PowerShell command: `Connect-MgGraph`

## Policy under test

| Setting | Configured value |
|---|---|
| Policy name | `Block-device-Authentication` |
| Included identity | Dedicated test user (Debbie O) |
| Excluded identity | Administrator account |
| Target resources | All resources |
| Condition | Authentication flows → Device code flow |
| Grant | Block access |
| Policy state | Report-only |

## Test approach

1. Connect to Microsoft Graph PowerShell using device-code authentication as the dedicated test user.
2. Confirm the connected account with `Get-MgContext`.
3. Locate the corresponding interactive sign-in event in Microsoft Entra sign-in logs.
4. Inspect the Conditional Access evaluation and Report-only result.
5. Confirm that the user, resource, and authentication-flow conditions match and that the Block grant control is evaluated.

See [configuration.md](configuration.md) and [test-results.md](test-results.md) for the detailed record.

## Outcome

The test-user sign-in to Microsoft Graph showed the expected policy match:
- Test user: Matched
- Resource: Microsoft Graph — Matched
- Authentication flows: Matched
- Grant control: Block
- Report-only result: Failure

In Report-only mode, the policy is evaluated but not enforced. The Report-only Failure result means the policy would have blocked the sign-in if it were enabled. It does not mean the policy itself caused the actual sign-in to fail.

## Safety note

The policy remains in Report-only mode. It has not been switched to On. Enforcement should only be considered after reviewing scope, confirming administrator exclusions, and validating a safe recovery path.

## Evidence

Screenshots are intended to be stored in the `screenshots/` folder. Remove or redact personal identifiers, tenant-specific details, and any secrets or temporary device codes before publishing evidence.
