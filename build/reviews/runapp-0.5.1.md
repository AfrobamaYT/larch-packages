# runapp 0.5.1-1, x86_64

- Provenance: c4rlo/runapp tag `0.5.1` on commit `1ba272ec2e7f` (2026-05-10);
  the recipe's sha256 equals the download.
- The local PKGBUILD is the AUR recipe of the upstream author with one change:
  the MIT LICENSE is installed, which the Makefile leaves out and a copy
  [larch] hands out has to carry.
- Capabilities (859 lines of C++): asks the person's systemd manager over
  D-Bus for a transient scope and execs the given program in it. Nothing else.
- Needed by: fm39hz (its keys run `runapp kitty` and the like).
- Dependencies: systemd-libs.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: MIT (LICENSE installed).
- Not done: a line-by-line reading; the four source files were read for what
  they start and where they connect.
- Release VM (release VM 3, 2026-10-01, base 033fc7cc upgraded to that day;
  after 34f77077): installed with `pacman -U`; fm39hz fetched complete and its
  terminal key opened kitty through runapp.
- Exact approved archive:
  `runapp-0.5.1-1-x86_64.pkg.tar.zst`, SHA-256
  `d05233c541dd7fc9a07507ad23438b4a6e0854c02ffc1ec6e6637df260f55581`.
  This approval covers no other version, architecture, or build.
