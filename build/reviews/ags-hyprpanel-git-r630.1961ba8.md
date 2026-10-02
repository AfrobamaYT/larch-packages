# ags-hyprpanel-git r630.1961ba8-2, x86_64

- Provenance: Jas-SinghFSU/HyprPanel
  `1961ba86ad5ab880beb639e5454054b2b5037e0d` (2026-04-22, signed by GitHub for
  the web merge), the last commit: the repository has been archived since, so
  upstream fixes nothing any more.
- The local PKGBUILD is the AUR recipe at `a900623` (2025-07-03), which built
  whatever `master` held, pinned to that commit, with three patches,
  bluetooth.py left out of the package, `npm ci --omit=dev --ignore-scripts`
  for `npm install`, and a `depends` naming the 13 Astal libraries HyprPanel
  imports instead of libastal-meta's 21. `pkgrel` is 2: the first build of the
  day had only the first patch and was never approved.
- The three patches, each against a way for someone else to run code or reach
  the machine:
  - notification-actions-invoke-only.patch: HyprPanel ran any notification
    action id containing `scriptAction:-` as a command when its button was
    clicked. The id is the sender's, and Firefox hands a web page's
    notification action through as `<action>-moz`
    (toolkit/system/gnome/nsAlertsIconListener.cpp;
    `dom.webnotifications.actions.enabled` is on by default), so a page
    allowed to notify could have one click run a command. Actions now only go
    back to the sender. HyprPanel's own snapshot and recording scripts use
    such actions to open the file; that button now does nothing, the file is
    still saved.
  - no-bluetooth-agent.patch: every start ran scripts/bluetooth.py, which
    registers itself as BlueZ's default agent (`NoInputNoOutput`) and answers
    RequestConfirmation, RequestAuthorization and AuthorizeService at once,
    before its Confirm/Deny notification is clicked. BlueZ takes a reply
    without an error as consent (src/agent.c, `simple_agent_reply`), so every
    pairing and service a device in range asked for was granted while
    HyprPanel ran; python-dbus, all it needs, comes with uwsm on every Larch
    system. Without it pairing from HyprPanel's menu works as from Larch's own
    panel ("Just Works", no agent).
  - wallpaper-path-as-argument.patch: the wallpaper path went into `bash -c`
    inside double quotes for `wal -i` and `matugen image`, so a picture whose
    name holds `$(...)` ran that as a command once pywal or matugen was
    switched on. The path is now an argument of its own.
- Capabilities of what remains (34,612 lines of TypeScript, 1,539 of scripts):
  - Commands from the person's configuration run through bash by design:
    custom modules, dashboard shortcuts and directories, power and profile
    actions, the restart command, hyprsunset.
  - The updates module polls with `checkupdates` and the AUR helper's `-Qum`;
    its left click opens a terminal that runs `sudo pacman -Syu`, then `paru
    -Syu` or `yay -Syu` (which builds unreviewed AUR updates) and `flatpak
    update -y` -- only when clicked, in a terminal the person sees.
  - Network: the clock menu's weather asks api.weatherapi.com for the
    configured location with the person's key -- also with none, the default,
    which fails with HTTP 401 (measured in the release VM); cover art through
    libastal-mpris; nothing else.
  - The instance socket and CLI (`hyprpanel <command>`) take window, theme,
    wallpaper, volume, media and notification commands from the person's own
    processes; none runs a command string.
  - No privilege: no setuid file, no service, unit or rule in the archive.
- Needed by: hyprland-unrounded, roccorakete-arch-dotfiles, n6v26r,
  shenghuipang, simboi, rudra.
- Dependencies: Arch's repositories (wireplumber, libgtop, bluez, bluez-utils,
  networkmanager, dart-sass, wl-clipboard, upower, gvfs,
  ttf-jetbrains-mono-nerd, gtksourceview3, libsoup3 and the rest of the AUR
  list), aylurs-gtk-shell and 13 libastal packages from this wave.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. The bundled JavaScript (base64 inside
  `/usr/share/hyprpanel/hyprpanel-app`) was decoded and checked: no
  `_initializeStartupScripts`, no `bluetooth.py`, no `wal -i` or `matugen
  image -q "` string; the first build still had all three. No file is setuid,
  setgid or group- or world-writable.
- Release VM, 2026-09-30 (fix proofs p16, p17 and p19): the wave's archives
  installed together with `pacman -U`; all eight rices that had stopped at
  these packages -- hyprland-unrounded, roccorakete-arch-dotfiles, n6v26r,
  shenghuipang, simboi, rudra, cyberarch and gitkhym -- fetched complete and
  switched there and back with their shells drawing (n6v26r and simboi after
  fixes of their own, dd4462bc and 6f989cc4). The first build (pkgrel 1) ran
  in p16 and p17; this one in p19 (hyprland-unrounded, n6v26r, simboi), where
  HyprPanel came up without the startup-script step whose bluetooth.py start
  the first build logged as an unhandled rejection.
- License: MIT.
- Not done: 34,612 lines were covered by greps for process starts, shells,
  network, files and D-Bus plus the code around every hit, not read line by
  line.
- Exact approved archive:
  `ags-hyprpanel-git-r630.1961ba8-2-x86_64.pkg.tar.zst`, SHA-256
  `6da4d32d3aae758e7386c538933d2ce60f6fd80f99bab850a2acd8b98a5ca446`.
  This approval covers no other version, architecture, or build.
