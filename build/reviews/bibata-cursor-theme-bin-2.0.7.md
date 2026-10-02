# bibata-cursor-theme-bin 2.0.7-1, any

- Provenance: `Bibata.tar.xz` of ful1e5/Bibata_Cursor release v2.0.7 (tag on
  commit `35ccfe209a80`); its sha256 equals the recipe's. Built by the
  project's own release workflow, not from source here.
- The local PKGBUILD is the AUR recipe at `5d418e2c` (Mark Wagie), unchanged.
- Contents: cursor themes only -- Bibata-Modern-{Amber,Classic,Ice} and
  Bibata-Original-{Amber,Classic,Ice}, each also -Right: Xcursor files and
  index.theme, 1,790 entries, 1,068 of them symlinks that all stay inside
  their theme; nothing executable.
- Needed by: the 34 rices whose switch said their Bibata cursor "is not
  installed" in the showcase runs of 2026-09-30/10-01, since [larch] no longer
  carries it -- among them hypr-nord, dotfile, hydradevx, leabua,
  mylinuxforwork, ml4w-lightcrimson-dotfiles, sadrach34, stephengunn,
  t4lentles5-dots.
- Dependencies: none.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: GPL-3.0-or-later.
- Not done: the cursor images were not compared against a build from source.
- Release VM (release VM 1, 2026-10-01, base 033fc7cc upgraded to that day):
  installed with `pacman -U`; hypr-nord fetched and switched, and the switch
  no longer said its cursor Bibata-Modern-Classic "is not installed", as it
  had in the showcase run of 18:46 without this archive.
- Exact approved archive:
  `bibata-cursor-theme-bin-2.0.7-1-any.pkg.tar.zst`, SHA-256
  `d2e01b69c270660f8623526ecf0cd70a290e52e246b5cc23d1d9e69a4595d9c4`.
  This approval covers no other version, architecture, or build.
