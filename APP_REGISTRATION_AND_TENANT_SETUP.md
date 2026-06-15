# App Registration and tenant setup

## 1. Create the application

In Microsoft Entra admin centre, create a new **App registration**.

- Name: `Copilot Studio Credits Monitor`
- Supported account types: **Accounts in this organisational directory only**
- Do not create a client secret.

Copy the following values from the Overview page:

- Application (client) ID
- Directory (tenant) ID

Both values are public identifiers and are entered by the user on the application's connection screen.

## 2. Configure the SPA Redirect URI

Open **Authentication**, select **Add a platform**, and choose **Single-page application**.

Add the exact Redirect URI shown by the application. Typical GitHub Pages examples are:

```text
https://organisation.github.io/repository/
https://organisation.github.io/
https://custom-domain.example/
```

The trailing slash matters. Do not configure the application as a Web platform and do not add a client secret.

## 3. Add Power Platform API permissions

Open **API permissions** and select **Add a permission**.

Choose **APIs my organisation uses** and search for **Power Platform API**. Confirm that its application ID is:

```text
8578e004-a5c6-46e7-913e-12f58912df43
```

Add these **delegated** permissions:

```text
Licensing.Allocations.Read
EnvironmentManagement.Environments.Read
ResourceQuery.Resources.Read
```

Grant tenant-wide admin consent when required by organisational policy.

## 4. Assign an appropriate administrative role

Power Platform API delegated permissions do not replace the signed-in user's Power Platform privileges. The user must have sufficient tenant administration rights to read licensing capacity, environment information and inventory. A Power Platform Administrator is the normal target role for this reporting application.

## 5. Deploy and connect

1. Deploy the `dist` output to GitHub Pages.
2. Open the deployed URL.
3. Confirm that the displayed Redirect URI exactly matches the SPA Redirect URI in Entra.
4. Enter the Client ID and Tenant ID.
5. Select **Connect** and complete the Microsoft sign-in flow.

## 6. Optional identifier storage

When **Remember Client ID and Tenant ID** is selected, only these two public identifiers are written to `localStorage`. Report data is never written there.

Without this option, the identifiers are kept in `sessionStorage` for the active tab session.

## 7. Consent and Conditional Access

The application uses delegated user authentication with Authorization Code Flow and PKCE through MSAL Browser. Conditional Access, user assignment requirements, device compliance rules and consent policies can affect sign-in.

Common configuration errors:

- Redirect URI mismatch.
- Permissions added to Microsoft Graph instead of Power Platform API.
- Application permissions selected instead of delegated permissions.
- Missing admin consent.
- Signed-in user lacks a Power Platform administrative role.
- Enterprise application has **Assignment required** enabled but the user is not assigned.
