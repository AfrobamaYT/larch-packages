# rofi-power-menu 3.1.0-2, any

- Provenance: jluttine/rofi-power-menu, tag `3.1.0` on commit `395c1e07360b`
  (2023-05-03), the newest release. The recipe's sha512 equals the download,
  and the unpacked tarball is identical to `git archive` of the tag.
- The local PKGBUILD is the AUR recipe at `5e499fa` (2026-03-31), unchanged,
  with the AUR's own fix-confirmation-msg.patch (one line: a zero-width space
  keeps the confirmation entries apart from the menu entries).
- Capabilities (300 lines of bash): a rofi/dmenu mode whose entries run
  `loginctl lock-session`/`terminate-session` for the current session and
  `systemctl suspend`/`hibernate`/`reboot`/`poweroff`, each after a
  confirmation; a choice is only compared with the fixed entries, never run,
  and custom entries are refused. Options go through getopt and `eval set --`,
  the standard form. No files, no network. The wrapper dmenu-power-menu runs
  `./rofi-power-menu` from the current directory when one is there; the rices
  call rofi-power-menu itself.
- Needed by: cachyos, stephengunn.
- Dependencies: rofi (Arch's repositories).
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable; the MIT
  text is installed.
- Release VM, 2026-09-30, installed from the image of that day with [larch]
  (fix proof p24): the wave's six archives installed with `pacman -U`; cachyos
  (stephengunn still waits for libinput-gestures), which had stopped at this
  package, fetched complete and switched there and back, as did the rest of
  the wave's eight rices.
- License: MIT.
- Not done: nothing -- both scripts were read whole.
- Exact approved archive:
  `rofi-power-menu-3.1.0-2-any.pkg.tar.zst`, SHA-256
  `72a87c6c4e35bbcdfad046484dbac0b97d014938d0d7b16a722d1b116244ea47`.
  This approval covers no other version, architecture, or build.
