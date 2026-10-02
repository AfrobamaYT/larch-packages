# hyprlax 2.2.7-1, x86_64

- Provenance: sandwichfarm/hyprlax tag `v2.2.7` on commit `6aaf8814fcc6`
  (2026-09-10); the recipe's sha256 equals the download, and the unpacked
  tarball is identical to `git archive` of the tag.
- The local PKGBUILD is the AUR recipe at `3207ce7` (2026-09-10), unchanged.
- Capabilities (C; 49,645 lines in the tarball with examples and tests): a
  parallax wallpaper on a background layer with OpenGL; `hyprlax ctl` talks to
  it over a socket in the runtime directory (`/tmp` only when XDG_RUNTIME_DIR
  is unset) to add and change layers. No network.
- Needed by: rice.
- Dependencies: wayland, mesa.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: MIT.
- Not done: greps for processes, sockets and network plus the code around
  every hit.
- Release VM, 2026-09-30, image of that day with [larch] (base 033fc7cc, proof
  run p25 on release VM 2): installed with `pacman -U`; rice fetched complete
  and switched there and back.
- Exact approved archive:
  `hyprlax-2.2.7-1-x86_64.pkg.tar.zst`, SHA-256
  `3259b58ab8b661642ec86f66ab8479ca9950e52b8c578bcde3e436c479b395a0`.
  This approval covers no other version, architecture, or build.
