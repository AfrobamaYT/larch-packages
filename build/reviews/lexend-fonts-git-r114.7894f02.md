# lexend-fonts-git 1:r114.7894f02-2, any

- Provenance: googlefonts/lexend `7894f02b2e7eabc48595f1d4eff3b17b48c6e651`
  (2023-03-02), the last commit of the repository.
- The local PKGBUILD is the AUR recipe at `adc286e` (2023-04-12), which built
  whatever the default branch held, pinned to that commit. `pkgver` reads what
  makepkg wrote into the file during the build.
- Contents: the repository's 80 TrueType fonts (8.6 MiB) and its OFL text.
- Needed by: brunoanesio.
- Dependencies: none.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: OFL-1.1.
- Not done: the fonts were taken as built by the project; nothing here rebuilt
  them from their sources.
- Release VM, 2026-09-30, image of that day with [larch] (base 033fc7cc, proof
  run p25 on release VM 2): installed with `pacman -U`; brunoanesio fetched
  complete and switched there and back.
- Exact approved archive:
  `lexend-fonts-git-1:r114.7894f02-2-any.pkg.tar.zst`, SHA-256
  `e73ef6c97c964c48ad8346b5c3d3ee12a425efae7aa582d99887470cc56aae52`.
  This approval covers no other version, architecture, or build.
