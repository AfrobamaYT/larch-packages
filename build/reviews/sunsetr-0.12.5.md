# sunsetr 0.12.5-1, x86_64

- Provenance: psi4j/sunsetr tag `v0.12.5` on commit `3261a3a9bbeb`
  (2026-08-10); the recipe's sha256 equals the download, and the unpacked
  tarball is identical to `git archive` of the tag.
- The local PKGBUILD is the AUR recipe at `201dc38` (2026-08-11), unchanged;
  cargo builds `--locked` from the repository's Cargo.lock.
- Capabilities (25,832 lines of Rust): sets the display's colour temperature
  through the Wayland gamma protocol or hyprsunset by the time of day for the
  location in its configuration; asks `pgrep` for other gamma tools; writes a
  debug log to `/tmp/sunsetr-debug-<pid>.log` only in debug mode. No network.
- Needed by: nespolibt.
- Dependencies: wayland (Arch's repositories).
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: MIT.
- Not done: greps for processes, files and network plus the code around every
  hit, not a line-by-line reading.
- Release VM, 2026-09-30, image of that day with [larch] (base 033fc7cc, proof
  run p25 on release VM 2): installed with `pacman -U`; nespolibt fetched
  complete and switched there and back.
- Exact approved archive:
  `sunsetr-0.12.5-1-x86_64.pkg.tar.zst`, SHA-256
  `c3807a3f7445982ed1808af7cec538f43ae1f01af0f6d03d8592c4939295d7a4`.
  This approval covers no other version, architecture, or build.
