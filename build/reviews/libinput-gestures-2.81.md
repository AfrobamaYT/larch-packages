# libinput-gestures 2.81-1, any

- Provenance: bulletmark/libinput-gestures tag `2.81` on commit `9552f0dd9b9e`
  (2025-12-02); the unpacked tarball is identical to `git archive` of the tag.
- The local PKGBUILD is the AUR recipe at `05c5bae` (2025-12-02) with the
  tarball's md5sum replaced by its sha256; the install script only prints
  notes.
- Capabilities (1,011 lines of Python): reads `libinput debug-events` and runs
  the command its configuration binds to a gesture (split with shlex, no
  shell). Reading input events needs the person in the `input` group, which
  Larch does not add anyone to; without it the gestures stay off.
- Needed by: stephengunn (with rofi-power-menu).
- Dependencies: python, libinput-tools, hicolor-icon-theme.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: GPL-3.0-or-later.
- Not done: greps for processes, files and network plus the code around every
  hit, not a line-by-line reading.
- Release VM, 2026-09-30, image of that day with [larch] (release VM 3 on
  2026-10-01, base 033fc7cc upgraded to that day; after 3c8108be): installed
  with `pacman -U`; stephengunn fetched complete and switched there and back.
- Exact approved archive:
  `libinput-gestures-2.81-1-any.pkg.tar.zst`, SHA-256
  `eaa9ee7b21c52fd7edc6435e94e601b50b1c7e6082d291198b6b9dc6d68358f1`.
  This approval covers no other version, architecture, or build.
