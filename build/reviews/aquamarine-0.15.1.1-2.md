# aquamarine 0.15.1.1-2, x86_64

- What it is: 0.15.1.1-1 (Arch's extra/aquamarine 0.15.1-1 with upstream's
  `fc77bd5` crash fix, see aquamarine-0.15.1.1.md) and one change of Larch's
  own, `headless-nested-parent-formats.patch`: in
  `CHeadlessBackend::getRenderFormats`, when no DRM backend answers, the
  Wayland backend's formats -- the parent compositor's dmabuf formats -- are
  returned before the fallback list. Nine added lines, one loop; nothing
  removed. hyprwm/aquamarine main has the same fallback (checked 2026-10-03,
  no issue or PR about it).
- Why: the offscreen rice sandbox draws on a headless screen inside a nested
  Hyprland. With no DRM backend the fallback list applied, and it holds linear
  buffers only (`DRM_FORMAT_INVALID` is 0, which as a modifier is LINEAR).
  NVIDIA renders into no linear buffer: on the owner's RTX 3080 the screen came
  up switched on at 0x0 ("GBM: Failed to allocate a GBM buffer: bo null",
  "REJECTED available mode 1920x1080@60.00Hz") and the sandbox photographed
  nothing. Implicit-modifier buffers allocated but were not renderable
  ("rbo: glCheckFramebufferStatus failed").
- Measured, the patched library loaded only into a nested Hyprland on that PC
  (same source and patches, built with makechrootpkg in the same chroot): the
  screen 1920x1080, buffers `BLOCK_LINEAR_2D`, no render errors, a grim
  picture of 14223 colours; the installed library gave 0x0 and nothing.
- Release VM (virtio, no render node) with this exact archive installed: the
  sandbox's screen 1280x800 with a picture, the host's monitors, workspaces,
  windows and pointer unchanged; rebooted with it, greeter and session came
  up. The portal's SIGSEGV in the greeter there predates it (six since 00:47
  that day, under Arch's 0.15.1-1) and xdg-desktop-portal-hyprland does not
  link aquamarine.
- A session on real screens is unchanged by construction: a DRM backend with
  formats still answers first, and the new loop is only reached without one.
- The recipe at `815ed5d1` differs from 0.15.1.1-1's in the header, `pkgrel`
  2, `pkgdesc` and the second patch in `source`, `sha256sums` and
  `prepare()`. Built with `tools/larch-packages build aquamarine` in the
  clean chroot ("patching file src/backend/Headless.cpp" in the log); its
  `.BUILDINFO` records the committed PKGBUILD's SHA-256 `890651392e53...`.
  It provides `libaquamarine.so=14-64` like -1. The `-debug` package the
  build also made is not published.
- ⛔ 0.15.2 from extra will replace it and does not carry this fix; on NVIDIA
  the sandbox then refuses with "LARCH-SANDBOX 0x0" (larch-rice 320743a0).
- Not measured: this exact archive on the owner's PC -- that needs his install.
- License: BSD-3-Clause (LICENSE installed).
- Exact approved archive:
  `aquamarine-0.15.1.1-2-x86_64.pkg.tar.zst`, SHA-256
  `1c13e53c0d80df27f259f4b339f36cb683838a6b6285f4af191dad2fbd2f7520`.
  This approval covers no other version or build.
