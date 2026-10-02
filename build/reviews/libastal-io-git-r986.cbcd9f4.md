# libastal-io-git r986.cbcd9f4-1, x86_64

- Provenance: Aylur/astal `cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e`
  (2026-09-23), the head of `main` on 2026-09-30, signed by kotontrion (RSA
  `3EBAA48009F1BBA5363A5E30A6D3CE93F1639450`; `git verify-commit` good against
  the key github.com/kotontrion.gpg publishes). Built from `lib/astal/io`.
- The local PKGBUILD is the AUR recipe at `c02a8d9` (2025-08-05), which built
  whatever the default branch held, with the source pinned to that commit.
  `pkgver`/`pkgrel` read `r986.cbcd9f4`/`1` because makepkg's `pkgver()` wrote
  them into the file during the build; the committed file is the one the
  archive's `.BUILDINFO` hashes. Nothing else differs from the AUR.
- Capabilities (1,146 lines of Vala):
  - Processes: `subprocess`/`exec` take an argv or split a string with
    `GLib.shell_parse_argv` -- no shell unless the caller runs one.
  - Files: read, write and monitor helpers for the calling shell.
  - The instance socket `$XDG_RUNTIME_DIR/astal/<instance>.sock` (inside the
    person's 0700 runtime directory) passes each request to the running
    shell's own handler; the `astal` tool lists instances, sends requests,
    toggles windows and quits them through it and the D-Bus interface
    `io.Astal.Application` (`quit`, `inspector`, `toggle_window` -- nothing
    that evaluates code).
  - No privilege: no setuid file, no D-Bus service, systemd unit, autostart
    entry, udev or polkit rule in the archive.
- Needed by: every Astal shell (AGS, HyprPanel).
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
  `libastal-io-git-r986.cbcd9f4-1-x86_64.pkg.tar.zst`, SHA-256
  `3eaaa026604470fbac21019d8a473188afe8d5b66f1762f42bf02621cbbaef7c`.
  This approval covers no other version, architecture, or build.
