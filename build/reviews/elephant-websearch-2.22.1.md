# elephant-websearch 2.22.1-1, x86_64

- Provenance: abenz1267/elephant tag `v2.22.1` on commit `8f1e21d6efe4`
  (2026-09-24); the recipe's sha256 equals the download; one source with
  elephant, built in the same chroot right after it, so the Go plugin and the
  daemon share their toolchain.
- The local PKGBUILD is the AUR recipe of the upstream author, unchanged.
- Capabilities (400 lines of Go): opens a search URL with the configured
  command (default xdg-open); the query is URL-encoded and the URL
  shell-quoted.
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
  kvdev25, and walker offered its Google entry for "fire".
- Exact approved archive:
  `elephant-websearch-2.22.1-1-x86_64.pkg.tar.zst`, SHA-256
  `73903f78d39de0b2eaa5618faa4f689a5e6dbb0829c72de82b571125f1812a48`.
  This approval covers no other version, architecture, or build.
