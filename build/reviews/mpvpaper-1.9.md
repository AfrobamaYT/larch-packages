# mpvpaper 1.9-1, x86_64

- Provenance: GhostNaN/mpvpaper, tag `1.9` on commit `131a52c266d2`
  (2026-07-18, unsigned), the newest release. The recipe's b2sum equals the
  download, and the unpacked tarball is identical to `git archive` of the tag.
- The local PKGBUILD is the AUR recipe at `722e4f1` (2026-07-19), unchanged.
- Capabilities (8,434 lines of C, a generated GL loader among them): plays a
  video through libmpv on a background layer surface. It loads mpv's own
  configuration (`config=yes`: `~/.config/mpv`); it checks with `system("pidof
  NAME")` for the program names in its own pause and stop lists (the person's
  configuration) and for five other wallpaper daemons (fixed names);
  `mpvpaper-holder` re-executes mpvpaper. Network only when it is given a URL
  to play.
- Needed by: garden-hyprland-dotfiles.
- Dependencies: mpv's libmpv and the Wayland client libraries (Arch's
  repositories).
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- Release VM, 2026-09-30, installed from the image of that day with [larch]
  (fix proof p24): the wave's six archives installed with `pacman -U`;
  garden-hyprland-dotfiles, which had stopped at this package, fetched
  complete and switched there and back, as did the rest of the wave's eight
  rices.
- License: GPL-3.0.
- Not done: greps for processes, files and network plus the code around every
  hit, not a line-by-line reading.
- Exact approved archive:
  `mpvpaper-1.9-1-x86_64.pkg.tar.zst`, SHA-256
  `ea6b80dfbf29776f1ea2d028f9168b239e1b17b745d899a6ba9c0f5a3710fccb`.
  This approval covers no other version, architecture, or build.
