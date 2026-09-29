# paru 2.1.0-2, x86_64

- Upstream tag `v2.1.0` dereferences to `70f66dc9eddb40e264ee6c9197541262b7792c9c`.
  The release tarball SHA-256 is
  `eea4dbb524db765d5316f540f9ee670c0bf81aae4827b5417eebb4c9b5651727`;
  the recipe pins it, and a fresh download for this review matched.
- Local PKGBUILD at `59649fdfb6c297f0501e9d0863b56fb339da3ee4` is the AUR
  recipe at `329be21` (2025-12-12) with one change: its `cargo update alpm
  alpm-utils` took whatever alpm release was newest on the day of the build,
  and is replaced by `cargo update -p alpm --precise 4.0.4`. Everything else
  resolves from the tarball's `Cargo.lock` (`cargo fetch --locked`,
  `cargo build --frozen`), which has no git dependencies.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `pkgbuild2`. The binary names the crates `alpm-4.0.4` and
  `alpm-utils-4.0.1` and links `libalpm.so.16`. `.PKGINFO` and the file list
  match the recipe: `/usr/bin/paru`, `/etc/paru.conf` (byte-identical to
  upstream's: `PgpFetch`, `Devel`, `Provides`, no `SkipReview`), man pages,
  shell completions and 23 translations. No setuid or group-writable file.
- By design paru downloads AUR recipes and runs makepkg on them, which is
  code nobody at Larch has read. Its own prompt shows each recipe before it
  builds; Larch keeps that prompt: `larch-rice` runs `paru -S --needed --aur`
  only in a terminal, never with `--skipreview` or `--noconfirm`
  (`tools/check-rice-supply-chain`).
- Not done: a line-by-line audit of paru's Rust source. The trust in it rests
  on its upstream, maintained by an Arch Linux developer
  (`morganamilo@archlinux.org`), and on the pinned, hashed tarball.
- Exact approved archive:
  `paru-2.1.0-2-x86_64.pkg.tar.zst`, SHA-256
  `3eebdc30d771426508605fbb6083f64daa49094ef8a3e91109d6838fbc07eb77`.
  This approval covers no other version, architecture, or build.
