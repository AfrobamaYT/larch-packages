# appmenu-glib-translator-git 25.04.r11.ga783b01-1, x86_64

- Provenance: vala-panel-project/vala-panel-appmenu
  `a783b01c8b653349843fac9bbd075dac52cdc9de` (2026-09-03, unsigned), the head
  of `master` on 2026-09-30; built from `subprojects/appmenu-glib-translator`.
- The local PKGBUILD is the AUR recipe at `8586fa2` (2026-03-12), which built
  whatever the default branch held, with the source pinned to that commit.
  `pkgver` reads `25.04.r11.ga783b01` because makepkg's `pkgver()` wrote it
  into the file during the build; the committed file is the one the archive's
  `.BUILDINFO` hashes. Nothing else differs from the AUR.
- Capabilities (2,766 lines of C): a library that turns
  `com.canonical.dbusmenu` menus into GMenuModel for the tray; no processes,
  files, sockets or network of its own, no privilege.
- Needed by: libastal-tray-git (HyprPanel, gitkhym). Arch's repositories have
  no appmenu-glib-translator; the package conflicts only with an
  `appmenu-glib-translator` of the same project.
- Dependencies: glib2.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable, and the
  archive holds no D-Bus service, systemd unit, autostart entry, udev or
  polkit rule.
- Release VM, 2026-09-30 (fix proofs p16, p17 and p19): the wave's archives
  installed together with `pacman -U`; all eight rices that had stopped at
  these packages -- hyprland-unrounded, roccorakete-arch-dotfiles, n6v26r,
  shenghuipang, simboi, rudra, cyberarch and gitkhym -- fetched complete and
  switched there and back with their shells drawing (n6v26r and simboi after
  fixes of their own, dd4462bc and 6f989cc4).
- License: LGPL-3.0 (the recipe says `LGPL3`).
- Not done: greps for processes, files and network plus the D-Bus handling
  that uses them, not a line-by-line reading.
- Exact approved archive:
  `appmenu-glib-translator-git-25.04.r11.ga783b01-1-x86_64.pkg.tar.zst`, SHA-256
  `3620767b6e24946f9e475f07b6eaee94eb21b2ee02c9e07e19c635a91964bdd1`.
  This approval covers no other version, architecture, or build.
