# hypr3d 0.5.0.r122.g205fe59-1, x86_64

- What it is: 0.5.0.r121.g5617153-1 (see hypr3d-0.5.0.r121.g5617153-1.md
  and the reviews it names) plus one commit on the fork's branch larch/main,
  AfrobamaYT/Hypr3D `205fe597fe9b66c04b2d01a6107c5aa417f42c16`. The GitHub
  archive of 205fe59 has SHA-256
  `3d552da4287bac9153b1f1ba077a9f51bc586bda2ae2221d66db004e230d943a`
  and holds exactly that commit's tree (compared file by file against
  `git archive`).
- Why: on 2026-10-08 after a visit to the room the owner's CS2, fullscreen
  before it, came back a floating 1920x1080 window over Steam's tiles on
  his AOC monitor: the tiles could not be clicked and new windows went
  under it.
- The commit, written in this session and read in full: the room saves a
  fullscreen window's state (Hyprland's fullscreen modes included) before
  it makes it a panel, puts the fullscreen back on leaving through
  Hyprland's fullscreen controller (out, then in: Hyprland still held it
  fullscreen), and while it flies out neither starts its own fullscreen
  passthrough nor moves the keyboard focus. The status file lists the
  saved layout. Nothing reads or writes other files, talks to the network
  or runs programs.
- The recipe at `b5f41fd0` differs from r121's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d`
  in the clean chroot against hyprland 0.56.2-4; its `.BUILDINFO` records
  the committed PKGBUILD's SHA-256 `5680060a1f9a...`, which matches. The
  archive holds the .so and the two licences; `ldd` finds every library.
  The `-debug` package is not published.
- Measured on this archive's `hypr3d.so` (SHA-256 `478d9cd3386b...`):
  `int3` instructions 0. In `larch-rice try --offscreen caelestia` with
  the owner's three monitors (span/fs-leak.sh): a fullscreen window over
  two tiles is fs=2 at 1920x1080 before and after a visit (r121: floating,
  not fullscreen); the resize states as with r121. The layout suite gives
  r121's result.
- Not fixed, measured: three tiles on one monitor come back in another
  order after a visit, with r121 too.
- License: unchanged, MIT (Hypr3D, Jolt; both installed), stb_image public
  domain, cgltf MIT; libjpeg-turbo, cairo and pango are linked, not
  included.
- Exact approved archive:
  `hypr3d-0.5.0.r122.g205fe59-1-x86_64.pkg.tar.zst`, SHA-256
  `344a131a80a4c8d51526aeea92a983bae0b4614c3bacca7e6b54277bc642ae74`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r121.g5617153-1.
