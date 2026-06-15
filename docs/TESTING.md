# Testing guide

## Published-site smoke test

1. Open the GitHub Pages URL.
2. Confirm that the header displays `v1.0`.
3. Confirm that the LinkedIn author control and ES/EN language controls are visible.
4. Change language and verify that labels update.
5. Select **Open test mode**.
6. Confirm that the completed capacity dashboard is displayed with a sample-data warning.
7. Navigate through Summary, Environments, Agents and About the data.
8. Generate the PDF report.
9. Download the static sample report.
10. Repeat the main flow at a mobile viewport or on a mobile device and confirm there is no horizontal scrolling.

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
- `tests/browser-flow-results.json`: headless Chromium flow through home, test mode, mobile layout and PDF download.
- `tests/sample-download-results.json`: file integrity and PDF signature checks.
- `TEST-REPORT.md`: consolidated human-readable summary.
