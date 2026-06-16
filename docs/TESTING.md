# Testing guide

## Published-site smoke test

1. Open the GitHub Pages URL.
2. Confirm that the homepage header matches the Power Platform Tenant Inventory Explorer pattern.
3. Confirm that the header displays `v1.0`, LinkedIn and the ES/EN language selector.
4. Confirm that the three progress stages are visible: Connection, Capacity and Insights.
5. Change language and verify that the homepage labels update.
6. Confirm that Client ID and Tenant ID appear side by side on desktop and stacked on mobile.
7. Select **Explore with demonstration data**.
8. Confirm that the completed capacity dashboard is displayed with a sample-data warning.
9. Navigate through Summary, Environments, Agents and About the data.
10. Generate the PDF report and download the static sample report.
11. Repeat the flow at 768 px, 390 px and 320 px and confirm there is no horizontal scrolling.

## Authenticated test

1. Enter a valid Application (Client) ID and Directory (Tenant) ID.
2. Authenticate with an authorised Power Platform administrator account.
3. Confirm that tenant capacity loads.
4. Confirm that environments and agents load.
5. Confirm that environments without explicit allocation display zero rather than a blocking error.
6. Generate the PDF and CSV exports.
7. Refresh information from the global header action.
8. Sign out and confirm that tenant data is removed from memory.

## Included automated evidence

- `tests/static-validation.json`: compiled-package and structural checks.
- `tests/browser-flow-results.json`: headless Chromium validation of the compiled homepage, responsive layout, localisation and demonstration-data flow.
- `tests/sample-download-results.json`: file integrity and PDF signature checks.
- `TEST-REPORT.md`: consolidated human-readable summary.
