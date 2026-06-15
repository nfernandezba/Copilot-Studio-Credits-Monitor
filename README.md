# Copilot Studio Credits Monitor

Static, read-only SPA for GitHub Pages that reports Microsoft Copilot Studio capacity using supported Microsoft Power Platform APIs.

## What it shows

- Purchased, allocated and consumed tenant capacity.
- Indicative remaining and unallocated capacity.
- A capacity-type selector with an **All capacity types** consolidated view when Microsoft returns more than one type.
- A per-capacity breakdown so the consolidated result remains transparent.
- Current capacity allocation by environment.
- Power Platform environment inventory.
- Copilot Studio agent inventory by environment.
- CSV and JSON exports generated locally in the browser.
- A standalone HTML report generated locally, including capacity, environments, agents and the books footer.
- Spanish and English book recommendations with local cover assets.

Consumption attribution by individual agent is intentionally out of scope.

> The consolidated view adds the numeric values returned for each displayed capacity type. Some capacity types can represent different units, so the application always shows the per-type breakdown alongside the consolidated result.

## Fastest deployment: GitHub Pages from the repository root

1. Upload **all files and folders in this package** to the root of the `main` branch.
2. Open **Settings → Pages** in the GitHub repository.
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Select branch **main** and folder **/(root)**.
5. Save and wait for GitHub Pages to publish the site.

The repository root already contains the compiled application:

```text
index.html
404.html
assets/
.nojekyll
```

No npm build is required for this deployment method.

## Alternative deployment: GitHub Actions

The repository also contains `.github/workflows/deploy-pages.yml` and the complete source code under `source/`.

To use this method, select **GitHub Actions** as the Pages source. Each push to `main` installs dependencies, runs tests, builds the application and deploys it.

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

The HTML report is assembled and downloaded locally in the browser. The application does not upload or retain a copy. Book covers are packaged as same-origin static assets and embedded into the downloaded HTML report as data URLs.

## Repository layout

```text
index.html                         Compiled application for branch deployment
404.html                           GitHub Pages fallback
assets/                            Compiled JavaScript, CSS, logo and book covers
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
npm ci
npm test
npm run dev
```

## Version

Current version: **0.2.0**

## Licence

MIT. See [LICENSE](./LICENSE).
