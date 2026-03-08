# Bump App Version

Bump an app's version, repackage, rebuild, and deploy.

Usage: /bump <app-name> [new-version]

If no new-version is given, auto-increment the patch version (e.g., 1.0.5 -> 1.0.6).

## Steps

1. **Read current version** from `<app-name>/Chart.yaml` and `<app-name>/OlaresManifest.yaml`.

2. **Bump version** in both files:
   - `Chart.yaml`: update `version` and `appVersion`
   - `OlaresManifest.yaml`: update `metadata.version` and `spec.versionName`

3. **Remove old chart** from `charts/` directory.

4. **Package new chart**: `helm package <app-name> -d charts/`

5. **Rebuild catalog**: `node scripts/build-catalog.js`

6. **Deploy**: `npx wrangler deploy`

7. **Verify**: Check the deployed API returns the new version:
   ```
   curl -s https://orales-one-market.aamsellem.workers.dev/api/v1/appstore/info?version=1.12.3
   ```

8. **Report**: Show old version -> new version, new hash, and deployed URL.

## Argument: $ARGUMENTS
