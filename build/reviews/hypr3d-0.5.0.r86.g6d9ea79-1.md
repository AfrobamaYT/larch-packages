# hypr3d 0.5.0.r86.g6d9ea79-1, x86_64

- What it is: 0.5.0.r84.g61bda92-1 (see hypr3d-0.5.0.r84.g61bda92-1.md and
  the reviews it names) plus two commits on the fork's branch larch/main,
  AfrobamaYT/Hypr3D `e9e2b4a` and `6d9ea796c8667916ca5595ecc308fedb686f5203`.
  The GitHub archive of 6d9ea79 has SHA-256
  `142a25915d52d0fa21a666674d3a07072a8abde7d6674613ce2599fd6c8c0f1b`
  and holds exactly that commit's tree (compared file by file against
  `git archive`).
- Why: the owner asked for portals as in VRChat, the games played last
  standing in the room, and a menu to spawn them and choose world,
  settings and model.
- The commits, written in this session and read in full:
  - `e9e2b4a`: `hl.plugin.hypr3d.portal(name, { image, command, at | front,
    yaw, width })` stands a picture on the floor; a player stepping into
    its middle runs the command once, not twice in 3 s, through
    `Config::Supplementary::executor()->spawn` -- Hyprland's own executor,
    the one `hl.exec_cmd` and an exec keybind use -- and a portal event
    goes out on socket2. The command comes from the caller of
    `hyprctl eval`, who can already run anything through `hl.exec_cmd`:
    no new authority. Pictures load through hyprgraphics in render; the
    scene shader gains an alpha cut.
  - `6d9ea79`: config `menu = { command, title }`; F1 in the room runs the
    command through the same executor, and the window with that title is
    brought to the eye in the F2 pose as it opens.
  - No file, thread, library or network call is added; processes start only
    as the caller's config says, through Hyprland's executor.
- The recipe at `9e7d70e6` differs from r84's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d` in
  the clean chroot against hyprland 0.56.2-4 (the source archive's checksum
  "Passed"); its `.BUILDINFO` records the committed PKGBUILD's SHA-256
  `7d5abedf2f49...`, which matches. The `-debug` package is not published.
- Measured in `larch-rice try --offscreen caelestia` (nested Hyprland 0.56.2
  on the owner's RTX 3080), on the Moon station, with fork builds and Larch's
  larch-games, larch-room and room-menu:
  - three portals from larch-games' faces stood on the deck's edge; a portal
    with `front = true` stood 2.5 m ahead facing the camera; walking into it
    ran its command 0.76 s after starting to walk, once, with the event;
    a missing portal or image fails with the reason;
  - F1 opened the menu window, which came to the eye at 1:1; the crosshair
    hovered and clicked its tiles: Fly switched flying on, Empty room and
    Moon station switched the world, a game's tile stood its portal and
    closed the menu; F1 again closed it;
  - this exact archive's `hypr3d.so` (SHA-256 `e0e67c90057621f9...`) on
    hyprland 0.56.2-3 as the owner's PC runs it: a front portal ran its
    command when walked into; F1 opened the menu; locked, `open()` printed
    "hypr3d: the session is locked".
- Not measured: the owner's real session and his three monitors with this
  build; a real game started from a portal (the sandbox ran test commands
  only, to start nothing on the owner's machine).
- License: unchanged, MIT (Hypr3D, Jolt; both installed), stb_image and
  font8x8 public domain, cgltf MIT; libjpeg-turbo is linked, not included.
- Exact approved archive:
  `hypr3d-0.5.0.r86.g6d9ea79-1-x86_64.pkg.tar.zst`, SHA-256
  `980ba2a5b1ad2af063e04671f3890b1b5d50c09493a056e52d15f9b12eaa66ee`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r84.g61bda92-1.
