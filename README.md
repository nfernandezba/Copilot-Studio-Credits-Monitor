# Copilot Studio Credits Monitor

**Public version: v1.0**

Static, read-only GitHub Pages SPA for reviewing Microsoft Copilot Studio capacity through supported Microsoft Power Platform APIs.

## Capabilities

- Purchased, allocated and consumed capacity at tenant level.
- Indicative remaining and unallocated capacity.
- Consolidated **All capacity types** view with a transparent per-type breakdown.
- Current capacity allocation by environment.
- Power Platform environment inventory.
- Copilot Studio agent inventory by environment.
- Local CSV exports for environments and agents.
- Local executive PDF generation.
- Test mode with fictional data and a downloadable sample report.
- Spanish and English interface.

Consumption attribution by individual agent is intentionally out of scope.

## Quick deployment

1. Upload the complete contents of this package to the root of the `main` branch.
2. In GitHub, open **Settings > Pages**.
3. Select **Deploy from a branch**.
4. Select branch **main** and folder **/(root)**.
5. Save and wait for publication.

No build process, GitHub Action, Node.js installation or source-code folder is required.

See [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md) for Microsoft Entra ID configuration and detailed deployment guidance.

## Test mode

Open the published application and select **Open test mode**, or append the following query string:

```text
?test=1
```

Example:

```text
https://your-account.github.io/your-repository/?test=1
```

Test mode does not authenticate, request tokens or call Microsoft APIs. It loads fictional data and enables the full dashboard and PDF report flow.

The static sample report is available at:

```text
assets/reports/Copilot_Studio_Credits_Monitor_Sample_Report_v1.0.pdf
```

## Privacy

The application has no backend or database. Functional report data remains in browser memory and disappears when the page is reloaded or closed. The optional remember setting stores only the public Application (Client) ID and Directory (Tenant) ID. Generated reports are created locally in the browser and are not uploaded or retained by the application.

## Repository structure

```text
/
├── index.html
├── README.md
├── LICENSE
├── .nojekyll
├── TEST-REPORT.md
│
├── assets/
│   ├── icons/
│   ├── images/
│   ├── reports/
│   ├── *.css
│   └── *.js
│
├── docs/
│   ├── DEPLOYMENT.md
│   └── TESTING.md
│
└── tests/
    ├── static-validation.json
    ├── browser-flow-results.json
    └── sample-download-results.json
```

## Licence

MIT. See [LICENSE](LICENSE).
