# ml4w-dotfiles-settings 2026.10.01-1, any

- Provenance: upstream `main` at commit
  `9199d4b76fafce81fe68aab67ee8f29136e4ec6d` (2026-10-01, unsigned), the
  newest. ML4W's own `setup.sh` installs `main` (`git clone --depth=1`), not
  the tag `0.2.0` (2026-03-18, five commits older): this is what an ML4W
  installation runs. The recipe's sha256 equals the download
  (`e36ea3cc3682592a2c734203723f68910004d086175923d63ba77e878b85e266`), and
  the unpacked tarball is identical to `git archive` of the commit.
- The PKGBUILD is Larch's own; no AUR recipe exists. It installs system-wide
  what ML4W's installer copies into the home, and points three paths from
  `~/.local` to the package's: `LIB_DIR` and `DEMO_FILE` in the script, the
  script's path in `SettingsWindow.qml`. Each edit is checked in `prepare()`,
  so a line that moved upstream stops the build. Nothing is downloaded during
  the build, nothing is compiled.
- What it installs: `/usr/bin/ml4w-dotfiles-settings` (bash, 387 lines) and
  `/usr/share/ml4w-dotfiles-settings/` with the Quickshell window
  (`shell.qml`, `SettingsApp/SettingsWindow.qml`, `CustomTheme/Theme.qml`, 511
  lines), `utils.sh` (99 lines) and `demo/settings.json`.
- Capabilities:
  - The window reads `~/.config/ml4w-dotfiles-settings/<profile>/settings.json`
    (the profile comes from `PROFILE`, which the rice's autostart sets) and
    its colors from `~/.local/share/ml4w-dotfiles-settings/colors/colors.json`.
    It answers the IPC targets `settings` (toggle) and `theme-manager`
    (reload).
  - A change runs the script with `--set --id ... --value ...` as arguments,
    not through a shell. The script writes the value into the file the
    settings entry names (overwrite, or an awk substitution of the entry's
    pattern), then runs the entry's `post_command` with `nohup bash -c` (the
    terminal mode, with gum, uses `eval`). These commands, the files and the
    folders the window lists with `ls` all come from the rice's
    settings.json: the rice's own code, which Larch already runs when the
    rice starts. The package adds no command of its own.
  - `--create <profile>` copies the demo settings into a new profile.
  - No network, no privilege, no service. Nothing runs unless the rice starts
    the window or the person calls the script.
- Dependencies: bash (core), gum, jq, quickshell (extra) -- all in Arch's
  repositories.
- Built with `makechrootpkg -c` in a clean chroot in the release VM
  `larch-release`, 2026-10-03; its `.BUILDINFO` records the sha256 of this
  PKGBUILD (`f2ef5958e821c694f283f937d29ebfc34859a09247b036af4653f08552c85eae`).
  The archive holds the files above and the license; no file is setuid or
  group-writable.
- Release VM, 2026-10-03: installed with `pacman -U` (gum and jq were already
  there). ML4W LightCrimson was prepared with its catalogue fix (`packages`,
  `post-install`) and switched to: 6 of 6 setup steps, 11 of 11 startup
  commands, and `qs list` showed the instance
  `/usr/share/ml4w-dotfiles-settings/quickshell/shell.qml`. "Dotfiles
  Settings" in the Welcome window opened "ML4W Dotfiles Settings" with the
  rice's values; switching on "Show Taskbar" rewrote the rice's
  `waybar_taskbar.sh` and `waybar/themes/ml4w-glass-center/config`, and
  waybar restarted with the taskbar. ML4W itself (`mylinuxforwork`), fetched
  fresh: 4 of 4 setup steps, 10 files pointed at the package and none left
  on `~/.local`; the IPC call its keys use opened the window in the rice's
  colors.
- License: GPL-3.0-only (`LICENSE` is the GPL v3 text; no file grants a later
  version).
- Exact approved archive:
  `ml4w-dotfiles-settings-2026.10.01-1-any.pkg.tar.zst`, SHA-256
  `7455c86ebac918618ff958b64715143e5d04ae077b7623f2896d6e84f43fa001`.
  This approval covers no other version, architecture, or build.
