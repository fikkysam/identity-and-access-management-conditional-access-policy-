# Lab 09 — Authentication Context

## Objective

Use a Microsoft Entra authentication context to apply stronger Conditional Access requirements to a sensitive operation inside an application, rather than applying the same requirements to every application sign-in.

This lab uses a small OpenID Connect (OIDC) test application that requests an authentication context for a protected operation. Merely creating a context and a Conditional Access policy does not trigger the policy; the application must request the context.

## Prerequisites and important boundaries

- Microsoft Entra ID P1 (or a subscription that includes it) for Conditional Access.
- A dedicated test identity: Don Paul (`don@fikayo.onmicrosoft.com`).
- A separate administrator identity excluded from the policy.
- An OIDC interactive web app registered in the same Entra tenant.
- Node.js and a code editor for the app integration stage.
- Do not use a production application or sensitive data for this lab.

Authentication context is intended for user-sign-in applications that use OpenID Connect/OAuth 2.0. App-only flows in which the application authenticates as itself are not supported for this feature. See Microsoft's developer guide: https://learn.microsoft.com/en-us/entra/identity-platform/developer-guide-conditional-access-authentication-context

## Important cleanup from previous lab

Before testing this lab, turn **Off** the Lab 07 policy `Block-NonCompany-Devices`. It targets All resources and can block Don Paul's browser session independently of this authentication-context policy. Keep the policy and its evidence; only disable it for this exercise.

Also confirm Lab 06 `restrict windows Access` remains Off.

## Phase A — Create an authentication context

1. Open Microsoft Entra admin center: https://entra.microsoft.com
2. Go to **Entra ID → Conditional Access → Authentication context** (under Manage).
3. Select **New authentication context**.
4. Set the display name to `Sensitive-Operation`.
5. Set the description to `Require stronger authentication before a user performs a sensitive operation in the lab application.`
6. Select **Publish to apps** so the application can request this context.
7. Save the context.
8. Record the generated context ID (for example, C1, C2, and so on). Do not assume it will be C1; use the actual ID created in this tenant.

## Phase B — Create the Conditional Access policy

1. Go to **Entra ID → Conditional Access → Policies → New policy**.
2. Name it `CA09-Require-MFA-Sensitive-Operation`.
3. Under **Users → Include**, select Don Paul.
4. Under **Users → Exclude**, select the administrator account.
5. Under **Target resources**, choose **Authentication context** (not All resources or a cloud app).
6. Select the exact context created in Phase A.
7. Under **Grant**, choose **Grant access → Require multifactor authentication**.
8. Keep the policy in **Report-only** while reviewing its configuration. Once the test app is ready, enable it for the one controlled end-to-end test. Keep the administrator exclusion.
9. Save the policy.

## Phase C — Register and configure the test application

The browser test must use an application that actually requests the authentication context. Signing in to My Apps or the Entra admin center alone is not a valid authentication-context test.

1. In Entra ID, open **App registrations → New registration**.
2. Name the app `Lab09-Authentication-Context-App`.
3. Choose the supported account type for this lab tenant (normally accounts in this organizational directory only).
4. Register the app and record its Application (client) ID and Directory (tenant) ID.
5. Add a Web redirect URI that matches the local Node.js app callback URL exactly (for example, `http://localhost:3000/auth/callback` for a local-only lab).
6. Configure the app to use an interactive OIDC authorization-code flow. Use a supported Microsoft identity library such as MSAL Node.
7. Do not put client secrets, certificates, tokens, or credentials into GitHub. For a local learning app, keep any secret in a local environment file excluded by `.gitignore`; prefer certificate-based credentials for production patterns.

## Phase D — Add the authentication-context request to the app

1. Implement an ordinary sign-in to the test app using OIDC.
2. Add a clearly labelled protected operation, such as **View sensitive lab record**. Do not connect it to real sensitive data.
3. When the user invokes that operation and the required context is not present, have the app request the tenant's recorded authentication-context ID using the OIDC claims request/claims-challenge mechanism described in Microsoft's developer guide.
4. Send the user through the Microsoft Entra authorization flow with that claims request.
5. Complete the MFA challenge when prompted.
6. On return, have the app verify the token's `acrs` claim contains the context ID required by the protected operation before allowing the operation.
7. If the claim is absent or validation fails, deny the protected operation. Do not rely on a front-end-only check.

Use Microsoft's official integration guide and sample as the implementation reference:
- https://learn.microsoft.com/en-us/entra/identity-platform/developer-guide-conditional-access-authentication-context
- https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-v2

## Phase E — One controlled test

1. Ensure Lab 06 and Lab 07 are Off.
2. Enable `CA09-Require-MFA-Sensitive-Operation` after confirming the target context and admin exclusion.
3. Open a private browser window and sign in to the Lab 09 test app as Don Paul.
4. Use an ordinary app page first. Confirm the app sign-in itself does not request the sensitive-operation context.
5. Invoke **View sensitive lab record**. The app should request the authentication context.
6. Complete MFA when prompted.
7. Confirm the app receives a token whose `acrs` claim contains the actual authentication-context ID and then allows the test operation.
8. In Entra **Monitoring & health → Sign-in logs**, locate the matching event and inspect the **Conditional Access** tab. Confirm the named policy and its result.
9. Capture the app result, authentication details, token claim evidence (redact tokens; capture only the relevant claim safely), and Conditional Access evaluation.

## Expected behavior

- Normal app sign-in: no authentication-context step-up is requested by the app.
- Sensitive operation: application requests the selected authentication context.
- Conditional Access policy: requires MFA for that context and test user.
- After successful challenge: app validates the returned `acrs` claim and allows the protected test operation.

These are expected results; record the actual results from the tenant and app rather than assuming success.

## Evidence checklist

- Authentication context created and **Publish to apps** enabled.
- Actual context ID recorded.
- Conditional Access policy targets that exact context.
- Don Paul included and administrator excluded.
- MFA grant control and policy state.
- App registration and redirect URI (no credentials or secrets).
- Protected operation requests the context.
- Token validation shows the required `acrs` value (never publish the full token).
- Matching sign-in log Conditional Access evaluation.

## Licensing and alternative integrations

Conditional Access requires Microsoft Entra ID P1. SharePoint can also consume authentication contexts, but applying contexts to SharePoint sites or sensitivity-labelled sites can require additional SharePoint Advanced Management and/or Microsoft 365 E5 compliance licensing. This lab therefore uses a custom OIDC user-sign-in app to avoid assuming those additional licenses.

## Cleanup

After evidence capture, decide whether to leave the policy On for the lab or turn it Off. Keep the app and context only in the non-production tenant. Remove any temporary credentials from local files and ensure those files are ignored by Git.
