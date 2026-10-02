# ttf-go 2.010-2, any

- Provenance: golang/image tag `v0.1.0` on commit `ffcb3fe7d1bf` (2022-10-17);
  the recipe's b2sum equals the download, and the unpacked tarball is
  identical to `git archive` of the tag.
- The local PKGBUILD is the AUR recipe at `21a42ca` (2026-05-21), unchanged;
  it installs only `font/gofont/ttfs/*.ttf` and their README as the licence.
- Contents: the Go fonts (TrueType).
- Needed by: flick0.
- Dependencies: none.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: BSD-3-Clause.
- Not done: nothing beyond checking what is installed.
- Release VM, 2026-09-30, image of that day with [larch] (base 033fc7cc, proof
  run p25 on release VM 2): installed with `pacman -U`; flick0 fetched
  complete and switched there and back.
- Exact approved archive:
  `ttf-go-2.010-2-any.pkg.tar.zst`, SHA-256
  `3697eb0891d2387a1e19e7c2c9f34d342377112bcf25d7708501d599152c2634`.
  This approval covers no other version, architecture, or build.
