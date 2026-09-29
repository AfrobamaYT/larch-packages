# arch-update 4.4.2-1, x86_64

- Upstream tag `v4.4.2` dereferences to `f4381b711a1bd81529a12790ee340a53a17a503a`.
  The release tarball SHA-256 is
  `c5d1af37a69ea0822f89d6c53485f05dcaf44d856725af2d9d8a6cd5b0c4e665`;
  the recipe pins it, and a fresh download for this review matched.
- Local PKGBUILD at `59649fdfb6c297f0501e9d0863b56fb339da3ee4` is the AUR
  recipe at `02244db` (2026-09-18) unchanged. `make` builds the tray applet
  with cargo from the tarball's `Cargo.lock` (no git dependencies), the man
  pages with scdoc and the translations; `check()` runs upstream's two bats
  tests (`version`, `help`), and both passed.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `pkgbuild2`. All 37 crate versions the tray binary names are
  the ones in `Cargo.lock`. The shell scripts in the package are
  byte-identical to the tarball's `src/`. `.PKGINFO` and the file list match
  the recipe: the command, its library scripts, the tray binary, a user
  service and timer that the package does not enable, desktop files,
  completions, man pages, 20 translations and 9 icons. No setuid file; the
  nine icons are mode 0664, as upstream's Makefile installs them, owned by
  root:root, and the group root has no member but root.
- By design it runs pacman, an AUR helper and flatpak, elevating with sudo,
  sudo-rs, doas or run0 when the person applies updates. It downloads Arch's
  news over HTTPS from `archlinux.org` with curl and prints them through
  htmlq; nothing downloaded is executed. It sources only its own scripts
  under `/usr/share/arch-update/lib`; its configuration file is read with
  anchored `grep` patterns and value whitelists, never sourced.
  `larch-update` runs it after taking a snapshot.
- Exact approved archive:
  `arch-update-4.4.2-1-x86_64.pkg.tar.zst`, SHA-256
  `8f8882d90421581164a449d24986754e4401761c3e7a18aeb0808f08405a70bd`.
  This approval covers no other version, architecture, or build.
