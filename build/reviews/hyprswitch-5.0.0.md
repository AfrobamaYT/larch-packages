# hyprswitch 5.0.0-1, x86_64

- Provenance: egnrse/hyprswitch tag `v5.0.0` on commit `43d29cda4acb`
  (2026-08-08); the recipe's sha256 equals the download, and the unpacked
  tarball is identical to `git archive` of the tag.
- The local PKGBUILD is the AUR recipe at `b16c634` (2026-08-12) with two
  changes: `arch` is x86_64 instead of any, since the package is a Rust ELF
  binary, and the tarball's MIT `LICENSE` is installed to
  /usr/share/licenses/hyprswitch, so its copyright line travels with every
  copy. cargo fetches `--locked` and builds `--frozen`.
- Capabilities (6,140 lines of Rust): a window switcher; it drives Hyprland
  through `hyprctl` -- dispatchers and `hyprctl eval` of the Lua submap it
  builds from its own options (keys, its own path). No network.
- Needed by: mujtaba-abd.
- Dependencies: hyprland, gtk4, gtk4-layer-shell.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: MIT.
- Not done: greps for processes and network plus the code around every hit.
- Release VM, 2026-09-30, image of that day with [larch] (base 033fc7cc, proof
  run p26 on release VM 1): installed with `pacman -U`; mujtaba-abd fetched
  complete and switched there and back.
- Exact approved archive:
  `hyprswitch-5.0.0-1-x86_64.pkg.tar.zst`, SHA-256
  `00983e34551b80d62d6ea6465b24f3b1731315b70383d7d33f3b1e4a717f3e76`.
  This approval covers no other version, architecture, or build.
