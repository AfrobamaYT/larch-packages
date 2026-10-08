# hypr3d 0.5.0.r121.g5617153-1, x86_64

- What it is: 0.5.0.r120.g91cbab6-1 (see hypr3d-0.5.0.r120.g91cbab6-1.md
  and the reviews it names) plus one commit on the fork's branch larch/main,
  AfrobamaYT/Hypr3D `56171536c20eda395e6c32253b20296328e0c576`. The GitHub
  archive of 5617153 has SHA-256
  `6b410ce2986b19f1d7d8c624d0bd817b187175ae22fbd4c6ca50a64876dc56f1`
  and holds exactly that commit's tree (compared file by file against
  `git archive`).
- Why: the owner's approved Claude Design draft "Room Interactions"
  (2026-10-08). Super + right drag grew a window faster with every frame
  and on by itself (measured: 960 -> 2883 px in eight equal mouse steps)
  and showed a blank slab while dragging; the waste bin wanted the
  crosshair exactly on it and the carried window near it at once.
- The commit, written in this session and read in full: the resize works
  the size out from the window's plane as it was at the grab, per axis;
  the room draws the frame (a new shader in GLScene, no new library) and
  asks the app once on release, holding the old frame until the app drew;
  the bin catches a carried window by the crosshair's angle to it. The
  world's drag now ends with its gesture. Nothing reads or writes files,
  talks to the network or runs programs; the only new client request is
  the one window size on release, as Hyprland's own resize sends.
- The recipe at `71102dd4` differs from r120's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d`
  in the clean chroot against hyprland 0.56.2-4 (the source archive's
  checksum "Passed"); its `.BUILDINFO` records the committed PKGBUILD's
  SHA-256 `5d4acebf9db7...`, which matches. The archive holds the .so and
  the two licences; `ldd` finds every library. The `-debug` package is not
  published.
- Measured on this archive's `hypr3d.so` (SHA-256 `6e883e23adf6...`):
  `int3` instructions 0, as in r120. In `larch-rice try --offscreen
  caelestia` (nested Hyprland 0.56.2-4, the owner's RTX 3080): Super on a
  corner shows its brackets; the grab does not jump (960 x 540); sideways
  only the width grows (1420 x 540), nodding only the height (1420 x 815);
  the app's minimum stops it in amber; Shift keeps the aspect; Esc sends
  nothing; a release asks once and foot draws 1392 x 696. The bin catches
  the carried window at 3.8 degrees, lets it go at 20, closes it on
  release; an app that refuses to close gets its window back at its own
  size.
- Not measured: an app's maximum size, several monitors.
- License: unchanged, MIT (Hypr3D, Jolt; both installed), stb_image public
  domain, cgltf MIT; libjpeg-turbo, cairo and pango are linked, not
  included.
- Exact approved archive:
  `hypr3d-0.5.0.r121.g5617153-1-x86_64.pkg.tar.zst`, SHA-256
  `e67667cfad7537f182b1403d8bdc5320705ab3f1e2641d5fdd3ccff4c7307294`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r120.g91cbab6-1.
