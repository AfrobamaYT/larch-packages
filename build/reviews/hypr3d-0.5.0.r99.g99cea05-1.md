# hypr3d 0.5.0.r99.g99cea05-1, x86_64

- What it is: 0.5.0.r87.g87c14c2-1 (see hypr3d-0.5.0.r87.g87c14c2-1.md and
  the reviews it names; staged, never sealed) plus twelve commits on the
  fork's branch larch/main, AfrobamaYT/Hypr3D
  `99cea05031a61deef408b07bc619675eb46a5235`. The GitHub archive of 99cea05
  has SHA-256
  `8ac241d7c17f58d29dde33457f43ad2cc2be28c1be0e63dc751ed11f1e5aad1f`
  and holds exactly that commit's tree (compared file by file against
  `git archive`).
- Why: the owner's batch of 2026-10-07 evening, released together with the
  larch package whose Backrooms world needs 99cea05 (its TV and lamp are
  black without it).
- The commits, written in this session and read in full: the waste bin
  (67c60f2), the spinbot fix (fd1fa6d), the following menu (75c04a0),
  shadows (7df5ba3), drawing only on change (a31fa6c), the HUD (278a577),
  the process gun (a5e87e5), floating windows keeping their size
  (cb996e0), runtime objects and pictures (fb17cff), head tracking
  (ddf5d6a), the TV zone and F8 (299bd37), the white fallback texture
  (99cea05). 1440 lines added in 8 files.
- What they add beyond drawing and input: one UDP socket for head tracking,
  bound to 127.0.0.1 only (INADDR_LOOPBACK), opened only when the config
  sets head.enabled (off by default), non-blocking, read in Hyprland's
  event loop, six doubles per datagram, others dropped. One `kill(PID,
  SIGKILL)`: the process gun held 1 s on the aimed window, PID from that
  window's client, never PID <= 1 or Hyprland's own. `hl.plugin.hypr3d.
  object()` reads a .glb path the user's own config names, through the
  existing model loader. No exec, no new library.
- The recipe at `59903396` differs from r87's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d`
  in the clean chroot against hyprland 0.56.2-4 (the source archive's
  checksum "Passed"); its `.BUILDINFO` records the committed PKGBUILD's
  SHA-256 `ceccb5d7533f...`, which matches. The `-debug` package is not
  published.
- Measured in `larch-rice try --offscreen caelestia` (nested Hyprland
  0.56.2-3 as the owner's PC runs it, on his RTX 3080) with this archive's
  `hypr3d.so` (SHA-256 `23d698f53a32...`): it loads; the Backrooms world
  (larch fefa2d54) opens at its spawn facing the TV, its windows show the
  sky; a foot window carried onto the TV is put on it (1724x1020),
  Super+wheel scales it to 1095x648, F8 uses it (pointer and click land),
  Super+F goes to 1920x1080 fullscreen and back onto the TV; the Moon
  station world loads with its sky and the walking player. The other
  features were each measured in the sandbox as they were committed
  (their commit messages name the measurements).
- Not measured: the owner's real three-monitor session with this build.
- License: unchanged, MIT (Hypr3D, Jolt; both installed), stb_image and
  font8x8 public domain, cgltf MIT; libjpeg-turbo is linked, not included.
- Exact approved archive:
  `hypr3d-0.5.0.r99.g99cea05-1-x86_64.pkg.tar.zst`, SHA-256
  `d062063220f40070ff97eec01867b30080a9983513ec8dddc0a636054a7af2c0`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r87.g87c14c2-1.
