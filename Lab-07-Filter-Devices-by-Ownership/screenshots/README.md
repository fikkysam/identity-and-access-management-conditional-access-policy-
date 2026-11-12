# Lab 07 — Screenshot Evidence

Add the configuration and test screenshots listed in the Lab 07 README to this folder. Use numbered, descriptive PNG filenames. The actual screenshots should only be committed after they have been captured from the tenant.

Suggested filenames:
- `01-lab06-policy-disabled-before-lab07.png`
- `02-test-user-inclusion-and-admin-exclusion.png`
- `03-target-resources-and-browser-client.png`
- `04-device-filter-include-mode.png`
- `05-device-ownership-rule-noncompany.png`
- `06-block-access-grant-and-enabled-state.png`
- `07-microsoft-sign-in-result.png`
- `08-conditional-access-policy-evaluation.png`

Expected filter rule:
`device.deviceOwnership -ne "Company"`

This negative operator is intentional: the test workstation was previously reported as Unregistered, and Microsoft Entra evaluates device properties as null for unregistered devices. A negative ownership operator can therefore match it. The test still needs to verify the policy-specific evaluation in sign-in logs.

Never upload passwords, tokens, recovery codes, or private keys.
