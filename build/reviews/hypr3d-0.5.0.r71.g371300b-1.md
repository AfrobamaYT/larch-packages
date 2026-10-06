# hypr3d 0.5.0.r71.g371300b-1, x86_64

- What it is: 0.5.0.r70.ge078c40-1 (see hypr3d-0.5.0.r70.ge078c40-1.md and the
  reviews it names) plus one commit on the fork's branch larch/main:
  AfrobamaYT/Hypr3D `371300bc10e6d43eaf34894c9738ca0ddb970846`. The GitHub
  archive of that commit has SHA-256
  `8d24d43d7d94abab9f148bca6458974028dcf8769744589f9a7ddc30d1f06e2b` ("Passed"
  in the build log).
- Why: the owner, 2026-10-06: every time the room was left, entering started
  over at the default position. Measured on e078c40: the view came back at
  yaw 0, pitch -0.2 and first person, and every window was laid out afresh in
  front of the player; only the position survived, because in first person
  the camera is read back from the player's body every frame and that
  overwrote the spawn placement.
- The commit (`371300b`: 162 lines added and 21 changed in `main.cpp`, 10 in
  the README), written in this session and read in full. It adds no file,
  process, network or library call, no thread and no persistent state outside
  the compositor's memory:
  - leaving the room remembers the eye, yaw, pitch, the view (F5) and the pose
    of every window and layer; entering restores them;
  - surfaces are matched by weak reference (`PHLWINDOWREF`/`PHLLSREF`), so a
    window closed in between does not hand its place to a new one at a
    reused address; surfaces not in the room (another workspace) keep what
    was remembered, closed ones are dropped;
  - `hl.plugin.hypr3d.reset()` and the dispatcher `hypr3d:reset` forget it and
    put camera and player body at the spawn point;
  - the status file (`/tmp/hypr3d-status.txt`, as before) gains a camera line
    and where each entity stands.
- The recipe at `d991c96d` differs from r70's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d` in
  the clean chroot against hyprland 0.56.2-4; its `.BUILDINFO` records the
  committed PKGBUILD's SHA-256 `f30288afa66e...`. The `-debug` package is not
  published.
- Measured. The owner's PC runs as Larch-B (12 GiB), where no VM may start, so
  everything ran in `larch-rice try --offscreen caelestia`: a nested Hyprland
  0.56.2 on his RTX 3080. Input came from a virtual keyboard (`wtype` 0.4-2,
  Arch's package, checked against the sync database, unpacked to a scratch
  directory only) and a virtual pointer (wlr-virtual-pointer through
  pywayland; the protocol XML from Arch's `wlr-protocols` package, checked the
  same way).
  - The sequence: walk, turn (yaw 0.75, pitch -0.5), third person, a window
    opened in the room, leave, enter.
  - With the plugin built from `371300b` by cmake, camera, player and all three
    windows came back identical; also with a toggle 0.15 s apart. `reset()`
    put camera and player at the spawn; left and entered after that, it kept
    the spawn.
  - The same sequence on e078c40 (only the status lines added) came back at
    yaw 0, pitch -0.2, first person, with every window moved.
  - This exact archive's `hypr3d.so` with three headless outputs in the
    owner's layout (1920x1080 at 0,0; 3840x2160 at scale 2 at 1920,45;
    1920x1080 at 675,-1080): three rounds of leave and enter, all 18 windows
    and layers, camera and player identical. Only Hyprland's 2D tile box of
    one terminal alternated by one pixel between rounds; its place in the
    room did not.
  - Unloading while the room was open: the nested Hyprland lived on (same
    PID). Loaded again, the room started at the spawn: the memory lives as
    long as the plugin is loaded.
- Seen but not caused by the plugin as far as measured:
  `xdg-desktop-portal-hyprland` dumped core (SIGSEGV) at 21:15:16, by its PID
  (351383, next to the sandbox's Hyprland 351170) the sandbox's own portal,
  and once at 20:47:46, before any of this ran. Not investigated.
- Not measured: his real three-monitor session; a window whose address is
  reused after it closed (the weak reference covers it by construction, not
  by a test).
- License: MIT (Hypr3D, Jolt; both installed), stb_image and font8x8 public
  domain, cgltf MIT; libjpeg-turbo is linked, not included.
- Exact approved archive:
  `hypr3d-0.5.0.r71.g371300b-1-x86_64.pkg.tar.zst`, SHA-256
  `dc92d937229e60adb3c331d60c107772a977d4ea2ba4799d041f73029ce0115f`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r70.ge078c40-1.
