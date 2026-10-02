# wleave 0.7.1-2, x86_64

- Provenance: AMNatty/wleave tag 0.7.1, commit
  `37e7cace1b30022f09465eace3f6298be6869ac1`.
- The local PKGBUILD is the AUR recipe at `923e200` (2026-07-26) with the
  source pinned to that commit instead of the movable tag; cargo fetches
  `--locked`.
- Capabilities (2,128 lines of Rust): a logout menu; each button runs the
  command its layout names (`sh -c`, from the rice's own layout.json); it
  installs a default style and layout in /etc/wleave. No network.
- Needed by: luyu-wu.
- Dependencies: librsvg, libadwaita, gtk4-layer-shell.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: MIT.
- Not done: greps for processes and network plus the code around every hit.
- Release VM, 2026-09-30, image of that day with [larch] (base 033fc7cc, proof
  run p25 on release VM 2): installed with `pacman -U`; luyu-wu fetched
  complete and switched there and back.
- Exact approved archive:
  `wleave-0.7.1-2-x86_64.pkg.tar.zst`, SHA-256
  `ac009f34c13b9f0487137d418d586757a877dbe286a491eb9b82baffb6799408`.
  This approval covers no other version, architecture, or build.
