# hypr3d 0.5.0.r102.g82ed203-1, x86_64

- What it is: 0.5.0.r100.g31512ed-1 (see hypr3d-0.5.0.r100.g31512ed-1.md and
  the reviews it names) plus two commits on the fork's branch larch/main,
  AfrobamaYT/Hypr3D `82ed203df8907c27aec43637af155ed6dc4a54d1`. The GitHub
  archive of 82ed203 has SHA-256
  `b553594643a0d40b735a87947dc0538f585861f6fdd5f4bffe1f326ba2bf3a98`
  and holds exactly that commit's tree (compared file by file against
  `git archive`).
- Why: on the owner's three monitors Super+F in the room did nothing
  visible for a window laid out on another monitor, and for two days his
  windows overlapped and turned floating after visits to the room (his
  foot and Brave both "tiled" over the whole of DP-3's workspace 5).
- The commits, written in this session and read in full: af03c29 moves a
  window that turns fullscreen on another spanned monitor while the room is
  open to the active workspace in front (Hyprland's own moveToWorkspace,
  silent) and back when its fullscreen ends; 82ed203 hands tiles back with
  Hyprland's own settiled (Config::Actions::floatWindow, disable) and saves
  a window new to the room with the floating state it had before. Hyprland
  actions only: no file, process, thread, library or network call is added.
- The recipe at `e0060340` differs from r100's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d`
  in the clean chroot against hyprland 0.56.2-4 (the source archive's
  checksum "Passed"); its `.BUILDINFO` records the committed PKGBUILD's
  SHA-256 `6588c1f1f246...`, which matches. The `-debug` package is not
  published.
- Measured in `larch-rice try --offscreen caelestia` (nested Hyprland
  0.56.2-4, as the owner's PC runs it since his login of 04:09, on his
  RTX 3080) with this archive's `hypr3d.so` (SHA-256 `2b66297a7100...`):
  - `.werkstatt/mondstation/tools/span/superf.sh`, his three monitors: a
    terminal laid out on the top monitor went from workspace 3 to
    workspace 1 in front, 1920x1080 fullscreen; "wasd hi" typed there
    reached it; Super+F again put it back on workspace 3 at 1808x1018.
  - `span/layout-leak.sh`, nine visits compared window by window: clean
    after open/close, Super+F twice, Super+wheel, F2, Super+F on the 4K
    monitor's window twice and with a close between; a window opened in
    the room came back as a tile beside its neighbour; the other two
    differences are the test's own last Super+F and a two-tile workspace
    laid out side by side again that was stacked before (re-admitted tiles
    get Hyprland's own split, not the one they had).
  - the one-monitor Backrooms TV test in a fresh sandbox: put on the TV
    1724x1020, Super+wheel 1095x648, F8, Super+F 1920x1080 and back.
- Not measured: the owner's real session with this build.
- License: unchanged, MIT (Hypr3D, Jolt; both installed), stb_image and
  font8x8 public domain, cgltf MIT; libjpeg-turbo is linked, not included.
- Exact approved archive:
  `hypr3d-0.5.0.r102.g82ed203-1-x86_64.pkg.tar.zst`, SHA-256
  `3633d9f8a63f075217c49f54a88eea8347d832549ebf2bf40a0a6179d30a2354`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r100.g31512ed-1.
