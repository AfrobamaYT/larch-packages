# pwvucontrol 0.5.3-2, x86_64

- Provenance:
  - Upstream tag `0.5.3` is a lightweight, unsigned tag on
    `fd5c9d1e5458b625d45e4159634b5b072f66cde1`. The download's b2sum equals
    the recipe's (sha256
    `5ac6db39d8bb347c3447592fbc923465c9e4b001da8e330861a215c964c74e27`), and
    its content equals `git archive fd5c9d1`; the tarball was regenerated
    byte-identically.
  - The tag moved once: the release of 2026-07-08 pointed at `018d913`
    (meson.build still said 0.5.2), and the tag was re-pointed on 07-14. The
    difference is the version string and Cargo.lock bumps (24 crate versions
    and the new build dependency `shlex` 2.0.1). The recipe's checksum pins
    the content of `fd5c9d1`.
- The local PKGBUILD is the AUR recipe at `66ec831` (2026-07-16) with the
  crates fetched before the build. Upstream's `src/meson.build` runs
  `cargo build --release` with `CARGO_HOME` in the build tree and without
  `--locked` or `--offline`, so the AUR build downloaded crates during
  build(). prepare() now runs `cargo fetch --locked` for the host target
  into that `CARGO_HOME`; build() and check() run with
  `CARGO_NET_OFFLINE=true`, so a crate the lock does not name fails the
  build.
- `Cargo.lock` holds 134 crates.io packages with checksums, plus
  `wireplumber` and `wireplumber-sys` from git at the locked commit
  `04fbbc6ea157cdd7061f6a5f2a6b22e102fccbcc` (arcnmx/wireplumber.rs plus two
  small saivert commits, dependency bumps and lifetimes; their diff was
  read). Of 29 build scripts, none downloads anything; the only processes
  they start are rustc probes and `sh -c command -v`. gettext-sys builds no
  bundled gettext (`gettext-system`). The meson wrap for blueprint-compiler
  is not fetched (`--wrap-mode nodownload`); Arch's blueprint-compiler 0.22.2
  is used.
- Capabilities:
  - No network, no process execution, no privilege, no persistence, no
    telemetry. No crate in the lock is a network library.
  - It changes PipeWire state, which is its job: device profiles and stream
    targets through WirePlumber's mixer and default-nodes APIs.
  - Its peak meters open monitor capture streams and present them as
    pavucontrol's (`src/ui/levelprovider.rs:43-52`), so the desktop's
    recording indicators do not list them. They read peak values only.
  - It writes only its GSettings (window size and flags).
  - It first tries to load `../data/resources/resources.gresource` relative
    to the working directory (`src/main.rs:74-75`): UI data from a relative
    path.
- Known advisories (RustSec advisory-db `f23b768`): `bitmaps` 3.2.1
  (RUSTSEC-2025-0167 unsound, RUSTSEC-2026-0247 unmaintained), `gettext-rs`
  0.7.7 (RUSTSEC-2026-0244 unsound), `imbl-sized-chunks` 0.1.3
  (RUSTSEC-2026-0292, double free when an element's drop panics). All in
  library code, none network-facing; exploitability was not analysed.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs` (Rust 1.98.1, meson 1.12.1), with `meson test`
  passing; the archive's `.BUILDINFO` records the sha256 of this PKGBUILD.
  The file list matches the recipe: `/usr/bin/pwvucontrol`, the desktop
  file, GSettings schema, icons, metainfo, translations and the gresource.
  The binary links glib, gtk4, libadwaita, graphene, wireplumber and
  libpipewire, all through its dependencies. No file is setuid or
  group-writable.
- Release VM, 2026-09-30: installed with `pacman -U` beside the other eight
  packages of this set and caelestia's six; it opened its window "Pipewire
  Volume Control".
- License: GPL-3.0-only as declared by the metainfo and the recipe; 26 source
  files carry GPL-3.0-or-later headers.
- Not done: the source of the 134 crates.
- Exact approved archive:
  `pwvucontrol-0.5.3-2-x86_64.pkg.tar.zst`, SHA-256
  `57a19aee93eb824917d6778b1aba02fec63b85e73ee76acc629ee6be6ebf2efe`.
  This approval covers no other version, architecture, or build.
