# Copilot Studio Credits Monitor

Static, read-only SPA for GitHub Pages that reports Microsoft Copilot Studio capacity using supported Microsoft Power Platform APIs.

## Features

- Purchased, allocated and consumed tenant capacity.
- Consolidated **All capacity types** view with transparent breakdown by type.
- Current capacity allocation by environment.
- Power Platform environment inventory.
- Copilot Studio agent inventory by environment.
- CSV exports for environments and agents.
- Multi-page PDF report generated locally in the browser.
- CoE Toolkit recommendations for Tenant Inventory Explorer and Environment Strategy Quick Assessment.
- Spanish and English book recommendations.

Consumption attribution by individual agent is intentionally out of scope.

## Publish with GitHub Pages

Upload every file and folder in this package to the root of the `main` branch. Then configure:

```text
Settings > Pages
Source: Deploy from a branch
Branch: main
Folder: / (root)
```

The repository root must contain `index.html` directly.

## Microsoft Entra ID

Register a single-tenant **Single-page application** and add the exact GitHub Pages URL, including the trailing slash, as a redirect URI.

Delegated Power Platform API permissions:

- `Licensing.Allocations.Read`
- `EnvironmentManagement.Environments.Read`
- `ResourceQuery.Resources.Read`

## Privacy

The application has no backend or database. Report data remains only in browser memory. The optional Remember setting stores only the public Application (Client) ID and Directory (Tenant) ID. PDF and CSV files are generated locally and the application does not retain copies.

## Version

0.3.0

## Licence

MIT. See [LICENSE](./LICENSE).
