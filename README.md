# H3X Searcher for Windows

[Download H3X Setup](https://github.com/lez337/H3Xexedl/releases/latest/download/H3X-Setup.exe)

The small black setup downloads the latest application package from this repository's public Releases. It includes the centered H3X logo, an installation-folder choice, download progress, Repair / Update, and Uninstall. The package size and SHA-256 checksum are verified before installation.

Install version 2.5.2 once with Setup → **Repair / Update** to enable in-app updates. Close H3X before using Setup. Your saved workspace and settings are retained.

Version 2.5.2 fixes local GHunt integration for the Python CLI, main.py and source folders. Version 2.5.1 adds a prominent live update-download card with percentage, downloaded/total size, progress stages and cancel/install controls. It also expands BrixHub and OathNet filters, adds clickable Telegram links and address actions, links map locations to person records, and adds a Google public-profile card when GHunt returns one. Startup updates, the persistent off switch and Telegram QR login are included. Requires Windows x64 and .NET Framework 4.8.

## Automatic updates

The installed Windows app checks the latest GitHub release at startup and downloads newer versions in the background. A download card remains visible while downloading and shows the new version, progress bar, percentage, downloaded/total size, and update stages. You can keep using H3X or cancel the download. Size and SHA-256 are verified before installation. Install version 2.5.1 to use this card for subsequent updates.

Click **Installer et redémarrer** when ready. H3X saves the workspace, closes, updates the same installation folder and restarts. It never forces a restart or installs an older version.

To turn automatic checks and downloads off, open **Paramètres → Intégrations → Mises à jour** and disable **Mises à jour automatiques au démarrage**. The switch saves immediately. **Vérifier maintenant** still works when automatic updates are off. A temporary connection failure does not prevent startup. Portable and development builds use Setup.

## Local GHunt setup

GHunt is a Python CLI, not a standalone desktop application. Follow [GHunt's official installation and authentication instructions](https://github.com/mxrch/GHunt).

Recommended installation in a terminal:

```text
python -m pip install pipx
pipx ensurepath
pipx install ghunt
ghunt login
```

Complete authentication with GHunt Companion, then restart H3X so it can see the updated PATH.

In **Settings → Local tools**, leave **Commande GHunt ou script main.py** empty to use the installed `ghunt` command. You can also enter a launcher path, select the source repository's `main.py`, or enter its folder. For source mode, choose the Python interpreter from the environment containing GHunt's dependencies. Authenticate in that same environment with `python main.py login` (using that interpreter).

H3X invokes `ghunt email <address> --json <temporary-output>`, or its equivalent through Python for source mode. No shell is used. GHunt and its Google session are not bundled or automatically installed; do not paste Google cookies into H3X. Availability checks run CLI help only and do not verify the Google session.

## Maps, Telegram links and Google profiles

Telegram result links open in the browser. Address fields have a **Carte** button: choose the matching place and optionally link the point to a saved dossier/person. In the map, choose a person to show all their locations; existing points can also be assigned to a person.

Email searches show a left-side Google card when configured and authenticated GHunt returns public profile data. It can show a display name, photo and a link to public Google Maps contributions/reviews. A display name is not a verified legal name. No profile or review availability is guaranteed. Geocoding uses the existing Photon/OpenStreetMap service.

## OathNet filters

Select OathNet in Search, choose the search mode, and expand **Filtres supplémentaires OathNet**.

- Common filters: email, email domain, username, phone, IP, Discord ID, country ISO code and city.
- Breach records: first name, last name, full name, region, postal code and source database.
- Exposure summaries: domain, subdomain, operating system, service and antivirus.
- Expanded supported identity/social/gaming fields, breach age and birth-date ranges, and endpoint-specific advanced controls are also available.

Password search fields are masked and omitted from saved request metadata. Reports using these fields must be searched again after reopening before fetching additional pages. This release does not resolve provider-side HTTP 403 or Cloudflare access challenges.

Set an inclusive date range using the indexing or compromise date. Choose relevance or index-date sorting, enable wildcard patterns when needed, and use the provider's default page size or 20, 50, 100 or 200 results per section.

Each report keeps its filter settings when you load the next page, using the same search session. A new main query clears previous filters. Invalid settings are rejected before initializing a session. Enrichment mode uses the main query without these search filters.

See [OathNet's structured-filter guide](https://docs.oathnet.org/guides/structured-filters) and [API reference](https://docs.oathnet.org/api-reference/v2-breach/search-breach-records). Automated tests use simulated provider responses and do not consume account lookups.

## BrixHub filters

In Search, select BrixHub and expand **Filtres supplémentaires**. All 43 documented BrixHub search fields are available, including names, contact information, birth-date components, address, company, vehicle and supported gaming identifiers. Blank fields are omitted; invalid or conflicting fields are rejected before sending a request.

Choose 10, 20, 50 or 100 results per page. Filters and page size remain applied when you explicitly load the next page. Changing the main query clears the previous additional filters.

The report sidebar includes an exact-age filter for **loaded results**. It uses a reported age or calculates age from a complete valid birth date; year-only and unknown dates are excluded. BrixHub has no documented native age parameter. Use birth-date fields before search when needed.

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

The release tag must be `v<version>` and match the manifest, for example `v2.5.2`. Drafts and prereleases do not feed the setup's `latest` URL.

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




