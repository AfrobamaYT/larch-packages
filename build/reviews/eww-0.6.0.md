# eww 0.6.0-1, x86_64

- Provenance:
  - Upstream tag `v0.6.0` is a lightweight tag on
    `d87c2fdbfdc012e76d229e4e9ea3325bc0f23e89` ("Release version 0.6.0"),
    the commit the recipe pins.
  - That commit is signed by `9EFD181455D31DD0F42DA932862BA3D7D7760F13`
    (elkowar, RSA-2048, 2024-04-21), one of the recipe's two `validpgpkeys`.
    `git verify-commit` confirmed it with a keyring holding only those two
    keys, and makepkg confirmed it again in the build. GitHub reports the
    commit as verified. The keyserver and GitHub serve the same key.
  - The recipe's b2sum for the Git source equals `git archive d87c2fd | b2sum`.
- The local PKGBUILD at `318a0024da34de008aa43ffe045ddeb6b6d77000` and
  `eww.install` are the AUR recipe at `756d212`, unchanged. `eww.install`
  only prints where the example config is.
- The recipe applies nixpkgs' `lockfile.patch` at `8b14399f`; its b2sum is
  the recipe's.
  - The patch changes only `Cargo.lock`: `time` 0.3.34 to 0.3.36,
    `time-macros` 0.2.17 to 0.2.18, and jaq-core's reference to `time`. That
    fixes the build with Rust 1.80 or later.
  - Both new checksums match the crates.io index.
  - nixpkgs wrote the patch for an earlier eww revision, but it applies to
    v0.6.0 without offset or fuzz. v0.6.0's lock differs from that revision
    only in `ahash` (0.7.8 there, 0.7.6 here, a version crates.io has yanked)
    and in eww's own version.
- After the patch, `Cargo.lock` holds 371 packages: 366 from the crates.io
  registry, all with checksums, and 5 workspace crates. There are no git or
  other registry sources, no `[patch]` or `[replace]`, and no
  `.cargo/config`. The build ran `cargo build --frozen`, and cargo re-locked
  nothing.
- Build scripts of eww's own crates:
  - `crates/eww/build.rs` reads the Git hash and date into the version string.
  - `simplexpr` and `yuck` run the lalrpop 0.20.0 parser generator on their
    grammar files. lalrpop has no build script and no process or network
    code.
- Capabilities:
  - eww runs the shell commands of the user's own config by design: widget
    handlers, `defpoll` and `deflisten`, each through `sh -c`.
  - Its `{}` placeholders are filled in without quoting
    (`crates/eww/src/widgets/mod.rs:44-54`). Some of the values come from
    outside the config: text typed into an `input` widget, and drag-and-drop
    data from other applications (`widget_definitions.rs:467,474,816-829`).
    A config that uses `{}` in such a handler can therefore be made to run
    shell code. The packaged example does not use either handler; Larch's
    Rice review reads each rice's handlers.
  - There is no HTTP or TLS crate in the tree and no TCP or UDP code in eww's
    crates.
  - It uses the session D-Bus only for its system tray.
  - Its IPC socket lives in `$XDG_RUNTIME_DIR`, which is private to the user.
  - It writes only its log under `~/.cache/eww`.
  - It uses no privilege.
- Known advisories in the locked tree (RustSec and OSV, checked 2026-09-29):
  - Vulnerabilities:
    - `bytes` 1.4.0, RUSTSEC-2026-0007: integer overflow in
      `BytesMut::reserve`;
    - `time` 0.3.36, RUSTSEC-2026-0009: stack exhaustion, only with RFC 2822
      formats, and eww's only user (jaq-core) uses ISO 8601;
    - `time` 0.1.45 (through chrono), RUSTSEC-2020-0071;
    - `crossbeam-epoch` 0.9.15, RUSTSEC-2026-0204: a `fmt::Pointer` impl;
    - `mio` 0.8.10, RUSTSEC-2024-0019, Windows only;
    - `rustix` 0.37/0.38, GHSA-c827-hfw6-qwvm.
  - Four crates are marked unsound: glib, tokio, rand and anyhow.
  - Seven are unmaintained, among them gtk-layer-shell.

  eww's inputs are the user's config, its private IPC socket, the session bus
  and drag-and-drop, all inside the user's own session. Whether any of these
  paths reaches the affected functions was not analysed, except for `time`.
- Built with `makechrootpkg -c` in a clean chroot in the disposable development
  VM `rice-pkgs` (Rust 1.98.1). `.PKGINFO` and the file list match the recipe:
  - `/usr/bin/eww`;
  - the `eww-bar` example under `/etc/xdg/eww`;
  - the MIT license.

  No file is setuid or group-writable.
- License: MIT.
- Not done: an audit of the 366 crates, their build scripts and proc-macros.
  Only lalrpop, lalrpop-util, jaq-core, time and time-macros were read.
- Exact approved archive:
  `eww-0.6.0-1-x86_64.pkg.tar.zst`, SHA-256
  `bccd75e02fd91d5fb10449960a73427dcfff5d562a9e721d10ac6fcbdf31e004`.
  This approval covers no other version, architecture, or build.
