# walker 2.17.1-2, x86_64

- Provenance: abenz1267/walker tag `v2.17.1` on commit `56c9e2b69e7d`
  (2026-09-24); the recipe's sha256 equals the download.
- The local PKGBUILD is the AUR recipe of the upstream author with two
  changes: cargo builds `--locked` from the tarball's Cargo.lock, and
  `depends` adds elephant, elephant-desktopapplications and
  elephant-providerlist -- walker 2 is only the window, waits for elephant's
  socket and shows nothing without a provider.
- Capabilities (7,916 lines of Rust): a GTK4 layer-shell launcher; asks
  elephant over its Unix socket ($XDG_RUNTIME_DIR/elephant/elephant.sock) and
  runs `elephant listproviders`; runs the preview and action commands of the
  person's own walker config through `sh -c`. No HTTP client among its crates,
  no network code.
- Needed by: arch-config, kvdev25.
- Dependencies: gtk4-layer-shell, poppler-glib, cairo; elephant and two
  providers.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: GPL-3.0 (LICENSE installed).
- Not done: greps for processes, files and network plus the code around every
  hit, not a line-by-line reading.
- Release VM (release VM 3, 2026-10-01, base 033fc7cc upgraded to that day;
  after 34f77077): installed with `pacman -U`; arch-config and kvdev25 fetched
  complete, switched, and their launcher key showed walker filled by elephant.
- Exact approved archive:
  `walker-2.17.1-2-x86_64.pkg.tar.zst`, SHA-256
  `a1db6e2b3e533c3c2b6eee8dcfdc0ab35b64e6193493b31373fed7beb5d9dd40`.
  This approval covers no other version, architecture, or build.
