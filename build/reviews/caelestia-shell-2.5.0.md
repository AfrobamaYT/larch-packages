# caelestia-shell 2.5.0-1.1, x86_64

- Provenance:
  - Upstream tag `v2.5.0` is an annotated, unsigned tag on
    `d999d4878ee4cec134168e60d913714566a8cfa6`. GitHub's web-flow key signed
    that commit, and it is in `main`'s history.
  - The recipe builds the release asset `caelestia-shell-v2.5.0.tar.gz`,
    uploaded by the project's release workflow. Its SHA-256
    `6bef9feff9f9c6afeb6fdf0b9bb1cfc3cfd7dff4c2a020e8079d6720975f3b6a` is the
    recipe's pin and GitHub's recorded digest.
- Asset against the tag: all 468 shared files are byte-identical, with the
  same modes.
  - Only in the asset: `REVISION`, which holds the tagged commit.
  - Only in the tag: the 23 files the release workflow excludes (dotfiles,
    `nix/`, `flake.*`).
- The local PKGBUILD at `4a78c687bdf0f897321b3d13702d2e38d966977a` is the AUR
  recipe at `d2c7b31` with three changes:
  - a comment header;
  - `pkgrel` 1.1;
  - Arch's `quickshell` in place of `quickshell-git`, which conflicts with
    the quickshell Larch's desktop runs on.

  Upstream's README asks for the Git build of quickshell. The run below is on
  Arch's 0.3.1.
- Processes:
  - The C++ plugin runs only fixed commands: `nvidia-smi`, `glxinfo` and
    `lspci` (`gpu.cpp:116-126`).
  - The QML runs brightness tools, `nmcli`, `hyprctl`, `xmllint`,
    `caelestia`, `wl-copy`, `swappy`, `pkexec wg-quick` for an opt-in VPN,
    and commands the user configures.
  - There is no `eval`, `new Function` or dynamic code loading.
  - The calculator places the typed text unescaped in a fish command
    (`CalcItem.qml:82`); only the user's own input reaches it.
- Network hosts:
  - **Every shell start:** `http://ip-api.com` in plain HTTP, when no weather
    location is configured, and every 15 minutes on the lock screen. This
    reveals the IP address and cannot be switched off; a configured location
    only replaces it with `geocoding-api.open-meteo.com` or
    `nominatim.openstreetmap.org` (`services/Weather.qml:55,166-227`).
  - **Weather, on location change and hourly:** `api.open-meteo.com`.
  - **Dashboard Media tab with a player active:** `lrclib.net` and
    `music.163.com`, both, whatever lyrics backend is chosen
    (`lyrics.cpp:392-394`). NetEase is sent a Firefox User-Agent.
  - **When cover art shows:** the album-art host and `img.youtube.com`.
  - **While an opt-in VPN is up:** a ping to `1.1.1.1`.
  - No telemetry and no update check.
- At its first start, with no recorded wallpaper, it runs
  `caelestia wallpaper -f <bundled wallpaper>` (`Wallpapers.qml:85-104`).
  That rewrites other programs' configs and makes caelestia-cli's `sudo -n`
  attempts (see its review), with no user action.
- Other defaults worth knowing:
  - The lock screen uses its own PAM files (`assets/pam.d`: `pam_faillock`,
    `pam_unix nullok`), so changes to `/etc/pam.d/system-auth` do not reach
    it.
  - Wi-Fi keys go to `nmcli` as arguments (`Nmcli.qml:456,480,494,701`).
  - Area screenshots stay in `/tmp/caelestia-picker-*.png`.
  - The title and body of unclosed notifications are kept in `notifs.json`.
  - Idle locks at 180 s, turns the screen off at 300 s and suspends then
    hibernates at 600 s.
- Build: CMake without FetchContent, ExternalProject or downloads. The recipe
  sets the version and revision, so no Git calls run.
- Run in the release VM (2026-09-29): the exact archives of this set were
  installed with `pacman -U` beside Arch's quickshell 0.3.1 and started with
  `qs -c caelestia` in the guest's session.
  - With qt6-m3shapes-git r38 the configuration did not load (see that
    package's review).
  - With r50 it drew its bar, border and bundled wallpaper: layers
    caelestia-background, caelestia-drawers and 4x
    caelestia-border-exclusion, and no QML load error.

  Not run: the caelestia Rice itself. Its switch still needs four more AUR
  packages: darkly-bin, papirus-folders, pwvucontrol and qtengine.
- Built with `makechrootpkg -c` in a clean chroot in the disposable development
  VM `rice-pkgs`; makepkg's SHA-256 check passed. `.PKGINFO` and the file list
  match the recipe:
  - the QML shell under `/etc/xdg/quickshell/caelestia`;
  - nine `Caelestia` QML plugins under `/usr/lib/qt6/qml/Caelestia`;
  - `/usr/lib/caelestia/version`;
  - the license.

  No file is setuid or group-writable.
- License: GPL-3.0. It bundles Google Sans Flex (OFL-1.1), `fuzzysort.js`
  (MIT) and `fzf.js` (BSD-3-Clause). Four images and `logo.svg` carry no
  licence statement.
- Not done:
  - a line-by-line reading of about 40,000 lines of QML and 20,000 of C++.
    They were grepped for network, process, privilege, file-write and eval
    patterns, and every hit was read;
  - the CVE status of libqalculate and quickshell.
- Exact approved archive:
  `caelestia-shell-2.5.0-1.1-x86_64.pkg.tar.zst`, SHA-256
  `c08acc6723cc42cac3af54728357f37b51381af366040546b2fd3a230a3f51cd`.
  This approval covers no other version, architecture, or build.
