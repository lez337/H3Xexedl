# H3X Searcher for Windows

[Download H3X Setup](https://github.com/lez337/H3Xexedl/releases/latest/download/H3X-Setup.exe)

The small black setup downloads the latest application package from this repository's public Releases. It includes the centered H3X logo, an installation-folder choice, download progress, Repair / Update, and Uninstall. The package size and SHA-256 checksum are verified before installation.

Install version 2.4.7 once with Setup → **Repair / Update** to enable in-app updates. Close H3X before using Setup. Your saved workspace and settings are retained.

Version 2.4.7 adds startup update checks and downloads, a persistent off switch, and combined BrixHub search filters. Telegram QR login and earlier authentication fixes are included. Requires Windows x64 and .NET Framework 4.8.

## Automatic updates

The installed Windows app checks the latest GitHub release at startup and downloads newer versions in the background. A progress banner shows the download; size and SHA-256 are verified before installation.

Click **Installer et redémarrer** when ready. H3X saves the workspace, closes, updates the same installation folder and restarts. It never forces a restart or installs an older version.

To turn automatic checks and downloads off, open **Paramètres → Intégrations → Mises à jour** and disable **Mises à jour automatiques au démarrage**. The switch saves immediately. **Vérifier maintenant** still works when automatic updates are off. A temporary connection failure does not prevent startup. Portable and development builds use Setup.

## BrixHub filters

In Search, select BrixHub and expand **Filtres supplémentaires**. Combine the main query with name, username, email, phone, mobile, IP, Discord ID, city, postal code, department, region, country, company, profession and role filters. Blank fields are omitted; invalid or conflicting fields are rejected before sending a request.

Choose 10, 20, 50 or 100 results per page. Filters and page size remain applied when you explicitly load the next page. Changing the main query clears the previous additional filters.

These fields use the [documented BrixHub search API](https://brixhub.to/api). No automatic pagination is performed.

## Telegram connection

### QR login

1. Close H3X and run Setup → **Repair / Update** to install version 2.4.6 or newer.
2. Open H3X's Telegram integrations and choose **Connexion par QR**. Previously saved API app credentials are reused. On first use, enter your own API ID and API Hash from [my.telegram.org/apps](https://my.telegram.org/apps).
3. On your phone, open Telegram → **Settings → Devices → Link Desktop Device**. Scan the QR shown in H3X and approve the H3X session.
4. If requested, enter your Telegram two-step password in H3X.

The QR image is generated locally and refreshes automatically during the three-minute login window. This flow does not request a code message. Cancelling or leaving the login panel stops the pending QR connection. An approved session uses H3X's existing protected storage.

The QR flow, worker transport and packaged storage have automated tests with simulated logins. A real account still needs the user's scan and approval. See [Telegram's QR-login protocol](https://core.telegram.org/api/qr-login).

### Code login

After updating, open Telegram settings in H3X and click **Recommencer**, then **Recevoir le code**. The API ID and API Hash identify your Telegram application; the login verification code is a separate value delivered by Telegram.

H3X now shows the delivery method reported by Telegram: an existing Telegram session, SMS, email, or a call. If the code is sent to Telegram, open the official Telegram conversation on your phone or another connected device. If Telegram offers another delivery method, use the resend button after its countdown. Some account verification steps must be completed in Telegram's official mobile app; H3X explains this when Telegram reports that requirement.

When Telegram asks for two-step authentication, enter only your Telegram password in the password step. H3X does not resubmit the already accepted code.

The login flows have automated tests with simulated Telegram responses. Actual code delivery still requires verification with your account. See [Telegram's authorization documentation](https://core.telegram.org/api/auth).

## Release files

Publish these four files together in a normal, latest GitHub Release:

- `H3X-Setup.exe` — the small online setup shared with users.
- `H3X-Searcher-Setup-<version>-x64.exe` — the complete application package; can also be installed offline.
- `h3x-release.json` — the exact versioned package URL, byte size and SHA-256 checksum.
- `SHA256SUMS.txt` — checksums for the published files.

The release tag must be `v<version>` and match the manifest, for example `v2.4.7`. Drafts and prereleases do not feed the setup's `latest` URL.

## Publishing the next update

In the local H3X source folder:

1. Increase the version in `package.json` and `package-lock.json`.
2. Run `BUILD-H3X-INSTALLER.bat`. It builds the app package, setup and manifest in a new `online-setup` folder.
3. Run `PUBLISH-H3X-GITHUB.bat`. It uploads the four files as a draft, verifies them and publishes the release. The GitHub CLI must be signed in to an account with write access.

For manual publishing, open [New release](https://github.com/lez337/H3Xexedl/releases/new), choose the matching version tag, attach the four files and publish it as the latest release.

Share the same permanent download link for every update:

[H3X-Setup.exe](https://github.com/lez337/H3Xexedl/releases/latest/download/H3X-Setup.exe)

Setup and the installed app use the same latest-release manifest. Publishing the four assets makes the new version available to startup update checks. No GitHub token is embedded in the setup or app.

See [GitHub's release guide](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository) and [permanent release links](https://docs.github.com/en/repositories/releasing-projects-on-github/linking-to-releases).


