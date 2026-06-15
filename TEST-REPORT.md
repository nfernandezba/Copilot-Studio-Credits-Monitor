# Test report

## Release

- Product: Copilot Studio Credits Monitor
- Public version: **v1.0**
- Deployment target: GitHub Pages, branch deployment from repository root
- Result: **Passed**

## Automated unit and integration tests

The source project was tested before producing this publication package.

- Test files: 7 passed
- Automated tests: 32 passed
- Failed tests: 0

Covered areas include:

- Power Platform API request handling and pagination.
- Capacity calculations and consolidated capacity types.
- Environment allocations, including environments without explicit allocation.
- Agent-to-environment association.
- Authentication and privacy constraints.
- Spanish and English localisation completeness.
- CoE Toolkit application shell and responsive rules.
- Test mode and sample datasets.
- Local PDF report generation.

## Compiled-package validation

All checks passed:

- `index.html`, `.nojekyll`, README and licence are present.
- The public version is `v1.0`.
- Compiled JavaScript and CSS are correctly referenced.
- Icon, image and report assets are present.
- No source code, dependency folders, build configuration or GitHub workflow is included.
- Every local resource referenced by `index.html` exists.

Detailed results: [`tests/static-validation.json`](tests/static-validation.json)

## Browser flow

A headless Chromium test completed the following flow successfully:

1. Load the compiled application.
2. Confirm HTTP 200 and visible `v1.0`.
3. Confirm ES and EN language controls.
4. Open test mode before authentication.
5. Confirm the complete sample dashboard.
6. Confirm the PDF generation action.
7. Download the static sample PDF.
8. Generate and download a PDF from the test dashboard.
9. Validate the 320 px mobile viewport without horizontal overflow.
10. Confirm there are no JavaScript console errors.

Detailed results: [`tests/browser-flow-results.json`](tests/browser-flow-results.json)

## Sample report integrity

- PDF signature: valid
- File size: 512,690 bytes
- SHA-256: `2b795f222c83150a8f4800735e046d43fdb07d2878b5ed198c65e12efb41fc7b`

Detailed results: [`tests/sample-download-results.json`](tests/sample-download-results.json)

## Build note

The production build completed successfully. The bundler reported a non-blocking warning for a JavaScript chunk larger than 500 kB. This is expected because the client-side PDF generation libraries are included in the static package. It does not prevent GitHub Pages deployment or application execution.
