# libastal-mpris-git r986.cbcd9f4-1, x86_64

- Provenance: Aylur/astal `cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e`
  (2026-09-23), the head of `main` on 2026-09-30, signed by kotontrion (RSA
  `3EBAA48009F1BBA5363A5E30A6D3CE93F1639450`; `git verify-commit` good against
  the key github.com/kotontrion.gpg publishes). Built from `lib/mpris`.
- The local PKGBUILD is the AUR recipe at `53495b5` (2026-06-22), which built
  whatever the default branch held, with the source pinned to that commit.
  `pkgver`/`pkgrel` read `r986.cbcd9f4`/`1` because makepkg's `pkgver()` wrote
  them into the file during the build; the committed file is the one the
  archive's `.BUILDINFO` hashes. Nothing else differs from the AUR.
- Capabilities (1,740 lines of Vala):
  - An MPRIS client (players, metadata, playback control) with the
    `astal-mpris` tool.
  - Cover art: a local file is used where it is; an http(s) URL is downloaded
    with libsoup, a `data:` URL decoded, any other URI copied through GIO --
    into `~/.cache/astal/mpris/<SHA-1 of the URL>`. The URL is the player's (a
    browser's media session: the page's own), so the download goes where that
    player already fetches from.
  - No privilege: no setuid file, no D-Bus service, systemd unit, autostart
    entry, udev or polkit rule in the archive.
- Needed by: HyprPanel, cyberarch, gitkhym.
- Dependencies: gdk-pixbuf2, glib2, glibc, json-glib, libsoup3 and quarrel.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`, in dependency order with the wave's own archives
  installed through `-I`. No file is setuid, setgid or group- or
  world-writable.
- Release VM, 2026-09-30 (fix proofs p16, p17 and p19): the wave's archives
  installed together with `pacman -U`; all eight rices that had stopped at
  these packages -- hyprland-unrounded, roccorakete-arch-dotfiles, n6v26r,
  shenghuipang, simboi, rudra, cyberarch and gitkhym -- fetched complete and
  switched there and back with their shells drawing (n6v26r and simboi after
  fixes of their own, dd4462bc and 6f989cc4).
- License: LGPL-2.1-only.
- Not done: the code was covered by greps for processes, sockets, D-Bus names,
  network and file writes plus the code that uses them, not read line by line.
- Exact approved archive:
  `libastal-mpris-git-r986.cbcd9f4-1-x86_64.pkg.tar.zst`, SHA-256
  `e4a9be985c09f408fdbd956a5969b3c656649f3f062e75eb71466d5166bb9a5b`.
  This approval covers no other version, architecture, or build.
