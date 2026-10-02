# nm-tray 0.5.1-1, x86_64

- Provenance: palinek/nm-tray tag `0.5.1` on commit `1d55df42144e`
  (2024-09-05); the recipe's sha256 equals the download, and the unpacked
  tarball is identical to `git archive` of the tag.
- The local PKGBUILD is the AUR recipe at `b4fb13b` (2024-09-13), unchanged.
- Capabilities (3,802 lines of C++/Qt): a NetworkManager tray menu over
  NetworkManagerQt; it starts nm-connection-editor to edit connections. No
  network of its own beyond NetworkManager's.
- Needed by: hyprland-dots.
- Dependencies: networkmanager-qt.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: GPL-2.0-or-later.
- Not done: greps for processes and files plus the code around every hit.
- Release VM, 2026-09-30, image of that day with [larch] (base 033fc7cc, proof
  run p25 on release VM 2): installed with `pacman -U`; hyprland-dots fetched
  complete and switched there and back.
- Exact approved archive:
  `nm-tray-0.5.1-1-x86_64.pkg.tar.zst`, SHA-256
  `61b39e60699c358385a2775019fa4ba41d889e43f8159e52ea9f91a177352f21`.
  This approval covers no other version, architecture, or build.
