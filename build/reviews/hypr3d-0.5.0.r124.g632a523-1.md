# hypr3d 0.5.0.r124.g632a523-1, x86_64

- What it is: 0.5.0.r123.gdb07af5-1 (see hypr3d-0.5.0.r123.gdb07af5-1.md
  and the reviews it names) plus one commit on the fork's branch larch/main,
  AfrobamaYT/Hypr3D `632a5230ef8d11ac2c7f6646aa9354656339b197`. The GitHub
  archive of 632a523 has SHA-256
  `77e6b5312925cdd3ac530b4c871d85b3b3bcef6eabf7a09da953a17c62c935da`
  and holds exactly that commit's tree (compared file by file against
  `git archive`).
- Why: the owner found the room laggy. His main monitor runs at 240 Hz.
  Measured in the rice sandbox with his three monitors: walking with the
  keys took 1.7 s for 240 frames, max 140 ms per frame.
- The commit, written in this session and read in full: every window and
  layer snapshot goes into a texture of its own size (glCopyTexSubImage2D
  out of the monitor-sized framebuffer, which is released at once),
  mipmapped there and kept while the size holds; a layer snapshot keeps the
  last one's picking mask instead of reading pixels back each time; the
  resize fade holds the old texture through hold/releaseHeld; the backdrop
  and the HUD sample the layers' own textures. The status file gains a
  frames: line and a framelog. Nothing reads or writes other files, talks
  to the network or runs programs.
- The recipe at `5d3b0c57` differs from r123's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d`
  in the clean chroot against hyprland 0.56.2-4; its `.BUILDINFO` records
  the committed PKGBUILD's SHA-256 `6e234aed1df7...`, which matches. The
  archive holds the .so and the two licences; `ldd` finds every library.
  The `-debug` package is not published.
- Measured on this archive's `hypr3d.so` (SHA-256 `556bf394be59...`):
  `int3` instructions 0. In `larch-rice try --offscreen caelestia` with the
  owner's three monitors, the main one at 240 Hz (span/frame-pace.sh):
  walking 240 frames in 1006 ms, p99 5.8 ms, none over 8 ms. A window
  hidden in the room leaves without a crash (unmap-crash.sh); a fullscreen
  window is fullscreen after a visit (fs-leak.sh). Pictures against r123:
  no further apart than r123 from itself (PSNR of three resize frames).
- Not measured: the owner's own machine with his windows.
- License: unchanged, MIT (Hypr3D, Jolt; both installed), stb_image public
  domain, cgltf MIT; libjpeg-turbo, cairo and pango are linked, not
  included.
- Exact approved archive:
  `hypr3d-0.5.0.r124.g632a523-1-x86_64.pkg.tar.zst`, SHA-256
  `565c9f86bfb7e9486fb6f6fdc34481aad514b524af181270f449b2f006b75ffb`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r123.gdb07af5-1.
