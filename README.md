# Copilot Studio Credits Monitor

Static, read-only SPA for GitHub Pages that reports Microsoft Copilot Studio capacity using supported Power Platform APIs.

## What it shows

- Purchased, allocated and consumed tenant capacity.
- Indicative remaining and unallocated capacity.
- Current capacity allocation by environment.
- Power Platform environment inventory.
- Copilot Studio agent inventory by environment.
- CSV and JSON export generated locally in the browser.

Consumption attribution by individual agent is intentionally out of scope.

## Fastest deployment: GitHub Pages from the repository root

1. Upload **all files and folders in this package** to the root of the `main` branch.
2. Open **Settings → Pages** in the GitHub repository.
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Select branch **main** and folder **/(root)**.
5. Save and wait for GitHub Pages to publish the site.

The repository root already contains the compiled application:

```text
index.html
assets/
.nojekyll
```

No npm build is required for this deployment method.

## Alternative deployment: GitHub Actions

The repository also contains `.github/workflows/deploy-pages.yml` and the complete source code under `source/`.

To use this method, select **GitHub Actions** as the Pages source. Each push to `main` will install dependencies, run tests, build the application and deploy it.

## Microsoft Entra ID setup

Register a **Single-page application** and add the exact GitHub Pages URL as a redirect URI, including the trailing slash. For example:

```text
https://your-organisation.github.io/your-repository/
```

Add these delegated Power Platform permissions:

- `Licensing.Allocations.Read`
- `EnvironmentManagement.Environments.Read`
- `ResourceQuery.Resources.Read`

Detailed instructions are available in [APP_REGISTRATION_AND_TENANT_SETUP.md](./APP_REGISTRATION_AND_TENANT_SETUP.md).

## Privacy

The application has no backend or database. Report data is held only in JavaScript memory and disappears when the page is reloaded or closed. The optional **Remember** setting stores only the public Application (Client) ID and Directory (Tenant) ID.

## Repository layout

```text
index.html                         Compiled application for branch deployment
assets/                            Compiled JavaScript, CSS and logo
.nojekyll                          Prevents Jekyll processing
.github/workflows/deploy-pages.yml Optional Actions deployment
source/                            Complete Vite source project and tests
README.md
LICENSE
SECURITY.md
TROUBLESHOOTING.md
APP_REGISTRATION_AND_TENANT_SETUP.md
```

## Local development

```bash
cd source
npm install
npm test
npm run dev
```

## Version

Current version: **0.1.3**

This version removes the unsupported `$top=250` parameter from the environment endpoint and accepts both array and OData `value` response formats.

## Licence

MIT. See [LICENSE](./LICENSE).
