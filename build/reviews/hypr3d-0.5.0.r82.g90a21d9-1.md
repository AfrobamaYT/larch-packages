# hypr3d 0.5.0.r82.g90a21d9-1, x86_64

- What it is: 0.5.0.r73.g8c1c758-1 (see hypr3d-0.5.0.r73.g8c1c758-1.md and
  the reviews it names) plus nine commits on the fork's branch larch/main,
  AfrobamaYT/Hypr3D `8c1c758..90a21d94300c21ab593746ae60f40c01ab32c148`.
  The GitHub archive of 90a21d9 has SHA-256
  `9ef77822cac711ab12f3c81e6d18f72f7db78885c366d4be78da2fe26787f21c`
  and holds exactly that commit's tree (compared file by file against
  `git archive`).
- Why now: r73 draws the room over a locked session (below, `4913b46`).
  The rest is the owner's wishes of 2026-10-07: movement that does not feel
  stiff, the AI teammate's eye, text legible in the room.
- The commits, read in full: 861 lines added and 85 changed in `main.cpp`,
  `GLScene`, `WindowCapture.cpp` and the README. All but `ee97ab1` were
  written in this session; `ee97ab1` comes from the AI teammate's session.
  - `ee97ab1`, merged as `aecda59`: a focus lock. F6 and
    `hl.plugin.hypr3d.focus_lock([bool])` keep the keyboard on the window
    that has it while the crosshair looks elsewhere; a click on another
    window still reaches it. It acts only while the room owns the input.
  - `8e070c6`: movement. Quake's ground friction and acceleration, a jump
    with coyote time, a buffer and variable height, Space twice toggles
    flight, Shift crouches, a landing dip, a sprint widening the view,
    respawn below -80 m, and `world.gravity` (clamped 0.5-40) handed to Jolt.
  - `971cbc7`: `companion("see")` draws the room once from the companion's
    eye, 768x432, into a framebuffer of its own and reads it back through a
    pixel pack buffer and a fence; the JPEG (libjpeg-turbo, already linked)
    goes to `$XDG_RUNTIME_DIR/hypr/$HYPRLAND_INSTANCE_SIGNATURE/hypr3d-sight.jpg`,
    written to `.part` and renamed, and a `sight` event on socket2 names it.
    That directory is the user's own (0700, Hyprland's sockets). One picture
    at a time, at most one a second; a picture that does not come back
    within 2 s, or a room that closes first, posts the error.
  - `295a5ff`: window polygons write no depth; the BSP already orders them.
    (Its message names the multi-monitor wall as the trigger; what was
    measured is one monitor, where a lone window and a rice's screen-sized
    layer stand at the same spot.)
  - `860c2f3`: every window snapshot gets mipmaps (`glGenerateMipmap` on
    the plugin-owned snapshot texture), up to 16x anisotropic filtering when
    the driver has GL_EXT_texture_filter_anisotropic, and windows are sampled
    with a -0.5 LOD bias.
  - `4913b46`: while `CSessionLockManager` reports the session locked, the
    room draws nothing, takes no input, is torn down from the event loop,
    and `open()`/`toggle()` fail with "hypr3d: the session is locked".
  - `9e3ae98`, `90a21d9`: F2 brings the aimed window to 1 m in front of the
    eye, scaled so one of its pixels covers one screen pixel, and back.
  - No process, thread, library or network call is added; the one new file
    is the sight JPEG above, written only when `companion("see")` asks.
- The recipe at `e6b8a3b6` differs from r73's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d` in
  the clean chroot against hyprland 0.56.2-4 (the source archive's checksum
  "Passed"); its `.BUILDINFO` records the committed PKGBUILD's SHA-256
  `1d691f31f1ae...`, which matches. The `-debug` package is not published.
- Measured, in `larch-rice try --offscreen caelestia` (nested Hyprland
  0.56.2 on the owner's RTX 3080), with builds of the fork by cmake:
  - Movement, sampled at 50 Hz: walking reaches 4 m/s in 0.15-0.3 s and
    stops in about 0.2 s; a tapped jump rises 0.45 m, a held one 1.05 m;
    `world.gravity = 5` gives 2.65 m on a 0.7 s hold.
  - The eye: a picture 35 ms after the frame that drew it, 38-46 KB; the
    frame drawing it costs 0.67-0.85 ms against 0.14 ms, the JPEG and file
    1.0-1.2 ms. Through larch-room-bridge, look to frame 53-54 ms; the AI
    teammate's session ran it with its real model, which described the
    picture correctly. A second look within a second is refused in 8 ms.
  - Depth: one foot window in an empty room at 5-40 m, invisible at all
    five distances before, visible at all five after.
  - Text: PSNR against an ideal downscale, bilinear -> with this build:
    10 m 26.60 -> 28.13 dB, 15 m 23.83 -> 26.65, 25 m 20.67 -> 23.00,
    40 m 18.92 -> 19.75. `glGenerateMipmap` on a 1920x1080 snapshot costs
    0.06 ms of GPU time (timer queries, standalone, same GPU).
  - Lock: caelestia locks with a WlSessionLock (ext-session-lock-v1).
    With r73's code, `open()` on the locked session showed a terminal and
    its text where the lock screen belongs; keys typed there reached the
    lock, not the terminal. With the fix: `open()` and `toggle()` print the
    error; open and then locked, the lock screen shows 0.5 s later and
    `companion("see")` answers "the room is closed"; unlocked, the room
    opens again. The sandbox's own idle lock later refused a test's open.
  - F2: the terminal covers 480,270 to 1440,810 in the room as in 2D,
    with no sub-pixel offset; 95.1 % of its inner pixels match the 2D
    window. The rest lies inside the text lines and does not change with
    mipmaps, anisotropy or foot's dpi-aware off: it comes from the snapshot
    every window goes through, not from F2 -- cause not found.
  - This exact archive's `hypr3d.so` (SHA-256 `0bf9918ef03e...`) in a fresh
    sandbox, on hyprland 0.56.2-3 as the owner's PC runs it: it loaded; the
    Moon station with walking and `world.gravity = 5` (a held jump 2.62 m,
    from the 4 Hz status); `companion("see")` posted its sight event; F2
    brought the aimed window to the eye and back; locked with the room
    open, the screen showed the lock screen, `open()` printed "hypr3d: the
    session is locked" and `companion("see")` "the room is closed";
    unlocked, the room opened again.
- Not measured: the owner's real session and its three monitors with this
  build; the pointer reaching windows behind a lock with r73 (keys did not).
- License: unchanged, MIT (Hypr3D, Jolt; both installed), stb_image and
  font8x8 public domain, cgltf MIT; libjpeg-turbo is linked, not included.
- Exact approved archive:
  `hypr3d-0.5.0.r82.g90a21d9-1-x86_64.pkg.tar.zst`, SHA-256
  `8e9a25d939343f310b6da9ca59fc46fe59374786065a77deb822c8460c5fbd6d`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r73.g8c1c758-1.
