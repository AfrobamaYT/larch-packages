# qtengine 0.2.2-1, x86_64

- Provenance:
  - Upstream tag `0.2.2` is an annotated, unsigned tag (`e43a0287`) on
    `167e7d9a27cdc8005ef2bd4d5d317b9da01b853f`, which GitHub reports as
    verified: 34 of the repository's 41 commits are SSH-signed with one
    ED25519 key, registered as kossLAN's GitHub signing key since
    2024-06-02.
  - The recipe's sha256 equals the download and `git archive 167e7d9`;
    `config.example.json` equals its pin.
  - Publisher: GitHub account kossLAN, repository created 2026-01-11.
    `platformtheme.cpp` derives from qt6ct (Ilya Kotov).
- The local PKGBUILD is the AUR recipe at `79a97c6` (2026-09-25) with the
  Qt6 half only (`-DBUILD_QT5=OFF`, and the Qt5/KF5 dependencies removed).
  The AUR build's Qt5 half installed to `/usr/lib/qt5/plugins`, where Arch's
  Qt5 never looks, and carried the relative RUNPATH `lib`: made loadable, it
  would search `./lib` in the working directory for its libraries first.
- Nothing is downloaded beyond the tarball. The plugin uses Qt private APIs,
  so it has to be rebuilt for every Qt update.
- What it is: a Qt platform-theme plugin and a proxy-style plugin, loaded
  into every Qt application that has `QT_QPA_PLATFORMTHEME=qtengine`, which
  Larch sets for caelestia.
  - It reads a JSON config (`$QTENGINE_CONFIG`, `$XDG_CONFIG_HOME`,
    `~/.config`, then `$XDG_CONFIG_DIRS` or `/etc/xdg`) and a colour-scheme
    file of any path through KConfig/KColorScheme. It never writes them.
  - The config selects an installed Qt style and a Qt Quick Controls style
    by name, resolved through Qt's normal plugin and QML paths; it never
    takes a library path.
  - Every Qt process tries to own the session name
    `org.qtengine.ConfigWatcher`, which exports one signal without payload
    and no methods. It watches the config and colour-scheme files with
    inotify.
  - No network, process execution, file writes, privilege, persistence or
    telemetry in `src/` (grep).
- `qtengine.install` only prints where the example config is.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; the archive's `.BUILDINFO` records the sha256
  of this PKGBUILD. The file list matches the recipe:
  `/usr/lib/libqt6engine-common.so`, the platform-theme and style plugins
  under `/usr/lib/qt6/plugins`, `/etc/qtengine/config.example.json` and the
  license. No RUNPATH. The platform-theme plugin links
  `libQt6QuickControls2`, from qt6-declarative, which the package does not
  list itself; it comes through `kconfig`, which depends on it. No file is
  setuid or group-writable.
- Release VM, 2026-09-30: installed with `pacman -U` beside the other eight
  packages of this set and caelestia's six; caelestia's Quickshell, started
  with `QT_QPA_PLATFORMTHEME=qtengine`, loaded `libqt6engine-plugin.so` and
  drew its background, border and drawers.
- License: BSD-2-Clause, installed. Ilya Kotov's BSD notice inside
  `platformtheme.cpp` is not shipped as a license file.
- Not done: whether current KF6 KConfig still lacks `$(...)` command
  substitution (removed in KF 5.61 for CVE-2019-14744).
- Exact approved archive:
  `qtengine-0.2.2-1-x86_64.pkg.tar.zst`, SHA-256
  `a7c64974a045d852007a3f0a6c362803c30a6f6dc7a21d3f6053d404f69be588`.
  This approval covers no other version, architecture, or build.
