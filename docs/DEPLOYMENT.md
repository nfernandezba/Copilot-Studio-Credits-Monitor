# Deployment

## GitHub Pages

Upload every file and folder in this package to the repository root. `index.html` must remain at the top level.

Configure GitHub Pages as follows:

- **Source:** Deploy from a branch
- **Branch:** main
- **Folder:** /(root)

The `.nojekyll` file must remain in the root so GitHub Pages serves all compiled assets without Jekyll processing.

## Microsoft Entra ID application registration

Create an application registration configured as a **Single-page application**.

Add the exact published GitHub Pages URL as a redirect URI, including the trailing slash:

```text
https://your-account.github.io/your-repository/
```

Add these delegated permissions for the Power Platform API:

- `Licensing.Allocations.Read`
- `EnvironmentManagement.Environments.Read`
- `ResourceQuery.Resources.Read`

Grant tenant consent where required by organisational policy.

The application asks the user to enter the public Application (Client) ID and Directory (Tenant) ID at runtime. Do not add a client secret or certificate to the repository.

## Updating the site

For a future compiled release, replace:

- `index.html`
- the complete `assets/` folder

Keep documentation and test evidence updated when the functional behaviour changes.

After publishing, confirm that the header displays **v1.0** and open the test mode using `?test=1`.
