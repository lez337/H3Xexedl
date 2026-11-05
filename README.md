# H3X Searcher for Windows

[Download H3X Setup](https://github.com/lez337/H3Xexedl/releases/latest/download/H3X-Setup.exe)

The small black setup downloads the latest application package from this repository's public Releases. It includes the centered H3X logo, an installation-folder choice, download progress, Repair / Update, and Uninstall. The package size and SHA-256 checksum are verified before installation.

After installation, run the same setup again to repair or update H3X. Close H3X before repairing or uninstalling. Your saved workspace and settings are retained.

Version 2.4.6 adds Telegram's supported QR login, while retaining code login and the earlier authentication fixes. Requires Windows x64 and .NET Framework 4.8.

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

The release tag must be `v<version>` and match the manifest, for example `v2.4.6`. Drafts and prereleases do not feed the setup's `latest` URL.

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
