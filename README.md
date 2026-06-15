# Copilot Studio Credits Monitor

![Version](https://img.shields.io/badge/version-v0.1.0-5552B4)
![Deployment](https://img.shields.io/badge/deployment-GitHub%20Pages-3895FF)
![Authentication](https://img.shields.io/badge/authentication-Microsoft%20Entra%20ID-27B8C6)
![Licence](https://img.shields.io/badge/licence-MIT-FFC000)

A static, read-only Single-Page Application for reviewing Microsoft Copilot Studio credit capacity, environment allocations and agent inventory through supported Microsoft Power Platform APIs.

## Capabilities

- Purchased, allocated and consumed Copilot Studio capacity at tenant level.
- Current credit allocation by Power Platform environment.
- Environment and Copilot Studio agent inventory.
- Local CSV and JSON export of the current session.
- Spanish and English interface.
- No backend, database or persistence of report data.

Consumption attribution by individual agent is intentionally out of scope.

## Deployment

Upload the repository contents to the root of a GitHub repository and configure GitHub Pages with:

```text
Source: Deploy from a branch
Branch: main
Folder: / (root)
```

The application calculates its redirect URI from the current GitHub Pages address.

## Microsoft Entra configuration

Create a single-tenant App Registration and add the GitHub Pages URL as a **Single-page application** redirect URI.

Grant these delegated permissions from **Power Platform API**:

```text
Licensing.Allocations.Read
EnvironmentManagement.Environments.Read
ResourceQuery.Resources.Read
```

Administrative consent and suitable Power Platform administrative roles may be required in the target tenant.

The user enters the Application (Client) ID and Directory (Tenant) ID when opening the application. These public identifiers can optionally be remembered in the browser. No client secret or certificate is used.

## Data and privacy

Report data is requested directly from Microsoft using the signed-in user's delegated access token and is held only in browser memory. Closing or reloading the page clears the functional dataset.

The application does not use a backend, database, IndexedDB or local storage for report results. Only language preference and, when explicitly requested, Client ID and Tenant ID may be stored locally.

## Files

```text
.nojekyll
index.html
README.md
LICENSE
assets/app.js
assets/app.css
assets/logo.svg
```

## Disclaimer

This is an independent, read-only reporting tool. It is not a Microsoft product and does not provide legal, compliance, security or licensing advice. Availability and completeness depend on Microsoft APIs, permissions, tenant roles, network controls and browser CORS support.

## Licence

Released under the [MIT Licence](LICENSE).
