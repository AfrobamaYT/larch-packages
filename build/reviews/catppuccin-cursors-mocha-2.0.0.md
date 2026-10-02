# catppuccin-cursors-mocha 2.0.0-1, any

- Provenance: the 16 `catppuccin-mocha-*-cursors.zip` assets of
  catppuccin/cursors release v2.0.0; each sha256 equals the recipe's. They are
  built by the project's own release workflow, not from source here.
- The local PKGBUILD is the AUR recipe at `99c0102` (2025-02-22), unchanged.
- Contents: cursor themes only -- Xcursor files, hyprcursor data (manifest,
  JSON, zipped SVG), index.theme; 3,360 files, none executable.
- Needed by: nyxiereal.
- Dependencies: none.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: GPL-2.0.
- Not done: the cursor images were not compared against a build from source.
- Release VM, 2026-09-30, image of that day with [larch] (base 033fc7cc, proof
  run p25 on release VM 2): installed with `pacman -U`; nyxiereal fetched
  complete and switched there and back.
- Exact approved archive:
  `catppuccin-cursors-mocha-2.0.0-1-any.pkg.tar.zst`, SHA-256
  `68b133f13a3ac0476e0df3980948283f68e8a92631e740628f2a907318f0cf16`.
  This approval covers no other version, architecture, or build.
