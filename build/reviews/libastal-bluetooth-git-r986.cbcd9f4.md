# libastal-bluetooth-git r986.cbcd9f4-1, x86_64

- Provenance: Aylur/astal `cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e`
  (2026-09-23), the head of `main` on 2026-09-30, signed by kotontrion (RSA
  `3EBAA48009F1BBA5363A5E30A6D3CE93F1639450`; `git verify-commit` good against
  the key github.com/kotontrion.gpg publishes). Built from `lib/bluetooth`.
- The local PKGBUILD is the AUR recipe at `8ec78d9` (2025-08-05), which built
  whatever the default branch held, with the source pinned to that commit.
  `pkgver`/`pkgrel` read `r986.cbcd9f4`/`1` because makepkg's `pkgver()` wrote
  them into the file during the build; the committed file is the one the
  archive's `.BUILDINFO` hashes. Nothing else differs from the AUR.
- Capabilities (786 lines of Vala):
  - A BlueZ client (adapters, devices, connect and pair through BlueZ's D-Bus
    API); it registers no pairing agent.
  - No privilege: no setuid file, no D-Bus service, systemd unit, autostart
    entry, udev or polkit rule in the archive.
- Needed by: HyprPanel.
- Dependencies: glib2, glibc.
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
  `libastal-bluetooth-git-r986.cbcd9f4-1-x86_64.pkg.tar.zst`, SHA-256
  `44991ea259f716c92a69087f2945665e4ec3c4f56d67404807934330a9538ba3`.
  This approval covers no other version, architecture, or build.
