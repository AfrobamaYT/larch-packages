# elephant-calc 2.22.1-1, x86_64

- Provenance: abenz1267/elephant tag `v2.22.1` on commit `8f1e21d6efe4`
  (2026-09-24); the recipe's sha256 equals the download; one source with
  elephant, built in the same chroot right after it, so the Go plugin and the
  daemon share their toolchain.
- The local PKGBUILD is the AUR recipe of the upstream author, unchanged.
- Capabilities (361 lines of Go): runs `qalc` with the typed query and shows
  its answer.
- Needed by: walker's default configuration (arch-config, kvdev25).
- Dependencies: libqalculate.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: GPL-3.0 (LICENSE installed).
- Not done: greps for processes, files and network plus the code around every
  hit, not a line-by-line reading.
- Release VM (release VM 3, 2026-10-01, base 033fc7cc upgraded to that day;
  after 34f77077): installed with `pacman -U`; elephant loaded it beside
  kvdev25, and walker answered 42 for "6*7" through it.
- Exact approved archive:
  `elephant-calc-2.22.1-1-x86_64.pkg.tar.zst`, SHA-256
  `08cbc4d17f9357fad19421ad99cf9b41e95acfbcf2d0f702bd9a9f284bbc183f`.
  This approval covers no other version, architecture, or build.
