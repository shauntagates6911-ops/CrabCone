# CrabCone Desktop

This folder contains helper files to package the CrabCone website as a Windows desktop application.

Files and purpose
- `main.js` - Minimal Electron entry that loads `index.html`.
- `package.json` - Electron build configuration and scripts.
- `icon.ico` - (optional) Windows icon file; place your .ico here to customize the app icon.
- `README.md` - (this file) instructions.

Local usage (Windows)
1. Clone the repository and open a PowerShell/Command Prompt in the `desktop/` directory.

2. Install dev dependencies:
   npm install

3. Run the app for testing:
   npm start

4. Build a Windows installer (electron-builder):
   npm run dist

   - This requires you to be on Windows (recommended) or to have Windows cross-compile tooling (Wine + makensis) configured on your runner.

Create a quick nativefier exe (alternative)
- Nativefier wraps a local folder or URL into a desktop app quickly. From the `desktop/` directory you can run:

  npm run nativefier

- That script runs nativefier to package the repo's parent folder (where `index.html` lives) into a native app. The produced folder will be placed in the current working directory.

CI (GitHub Actions)
- A workflow is provided at `.github/workflows/windows-build.yml` that runs on `windows-latest`, installs dependencies, runs `npm run dist` (electron-builder) and runs Nativefier as an alternative, uploading artifacts.

Notes and troubleshooting
- Ensure `index.html` and any needed assets are available in the build output. If you change the repo layout, update `desktop/main.js` or the build config accordingly.
- Provide an `icon.ico` in the repository root if you want a custom Windows icon; both Electron and Nativefier commands reference `../icon.ico`.
- If electron-builder fails because of missing system tooling (makensis), prefer building locally on Windows or use GitHub-hosted Windows runner.
