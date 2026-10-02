# elephant-providerlist 2.22.1-1, x86_64

- Provenance: abenz1267/elephant tag `v2.22.1` on commit `8f1e21d6efe4`
  (2026-09-24); the recipe's sha256 equals the download; one source with
  elephant, built in the same chroot right after it, so the Go plugin and the
  daemon share their toolchain.
- The local PKGBUILD is the AUR recipe of the upstream author, unchanged.
- Capabilities (181 lines of Go): lists the installed providers for walker's
  provider menu.
- Needed by: walker's default configuration (arch-config, kvdev25).
- Dependencies: none.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: GPL-3.0 (LICENSE installed).
- Not done: greps for processes, files and network plus the code around every
  hit, not a line-by-line reading.
- Release VM (release VM 3, 2026-10-01, base 033fc7cc upgraded to that day;
  after 34f77077): installed with `pacman -U`; elephant loaded it beside
  kvdev25 (`elephant listproviders` names it).
- Exact approved archive:
  `elephant-providerlist-2.22.1-1-x86_64.pkg.tar.zst`, SHA-256
  `7011b2586bc1bc9f3244cafd21f1ab174a103fa43a97a769505ac147e1df367b`.
  This approval covers no other version, architecture, or build.
