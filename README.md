# H3X Searcher for Windows

[Download H3X Setup](https://github.com/lez337/H3Xexedl/releases/latest/download/H3X-Setup.exe)

The small black setup downloads the latest application package from this repository's public Releases. It includes the centered H3X logo, an installation-folder choice, download progress, Repair / Update, and Uninstall. The package size and SHA-256 checksum are verified before installation.

After installation, run the same setup again to repair or update H3X. Close H3X before repairing or uninstalling. Your saved workspace and settings are retained.

Version 2.4.4 includes the Telegram login fix for account data-center redirects. Requires Windows x64 and .NET Framework 4.8.

## Release files

Publish these four files together in a normal, latest GitHub Release:

- `H3X-Setup.exe` — the small online setup shared with users.
- `H3X-Searcher-Setup-<version>-x64.exe` — the complete application package; can also be installed offline.
- `h3x-release.json` — the exact versioned package URL, byte size and SHA-256 checksum.
- `SHA256SUMS.txt` — checksums for the published files.

The release tag must be `v<version>` and match the manifest, for example `v2.4.4`. Drafts and prereleases do not feed the setup's `latest` URL.

## Publishing the next update

In the local H3X source folder:

1. Increase the version in `package.json` and `package-lock.json`.
2. Run `BUILD-H3X-INSTALLER.bat`. It builds the app package, setup and manifest in a new `online-setup` folder.
3. Run `PUBLISH-H3X-GITHUB.bat`. It uploads the four files as a draft, verifies them and publishes the release. The GitHub CLI must be signed in to an account with write access.

For manual publishing, open [New release](https://github.com/lez337/H3Xexedl/releases/new), choose the matching version tag, attach the four files and publish it as the latest release.

Share the same permanent download link for every update:

[H3X-Setup.exe](https://github.com/lez337/H3Xexedl/releases/latest/download/H3X-Setup.exe)

Setup checks the latest release when the user chooses Install or Repair / Update. It does not silently update the app in the background. No GitHub token is embedded in the setup.

See [GitHub's release guide](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository) and [permanent release links](https://docs.github.com/en/repositories/releasing-projects-on-github/linking-to-releases).
