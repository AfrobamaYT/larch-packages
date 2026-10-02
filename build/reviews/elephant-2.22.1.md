# elephant 2.22.1-1, x86_64

- Provenance: abenz1267/elephant tag `v2.22.1` on commit `8f1e21d6efe4`
  (2026-09-24); the recipe's sha256 equals the download.
- The local PKGBUILD is the AUR recipe of the upstream author, unchanged; `go
  build -trimpath`, modules as go.sum pins them.
- Capabilities (5,538 lines of Go outside the providers): a data-source daemon
  that loads its providers (Go plugins in /usr/lib/elephant) and answers
  walker over a Unix socket; runs the `before_load` commands of the person's
  elephant config; keeps a history cache. `elephant service enable` writes and
  enables a systemd user unit and `elephant community install` clones
  github.com/abenz1267/elephant-community -- only when a person runs those
  subcommands. No network otherwise.
- Needed by: walker (arch-config, kvdev25).
- Dependencies: none at run time.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: GPL-3.0 (LICENSE installed).
- Not done: greps for processes, files and network plus the code around every
  hit, not a line-by-line reading.
- Release VM (release VM 3, 2026-10-01, base 033fc7cc upgraded to that day;
  after 34f77077): installed with `pacman -U`; walker found it running beside
  arch-config and kvdev25.
- Exact approved archive:
  `elephant-2.22.1-1-x86_64.pkg.tar.zst`, SHA-256
  `e5971ddf766c9508ce79a6f5e1c951a60182ee82a07d54c7c96442d0e6a4c4f6`.
  This approval covers no other version, architecture, or build.
