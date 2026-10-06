# hypr3d 0.5.0.r70.ge078c40-1, x86_64

- What it is: 0.5.0.r67.g3656ac7-1 (see hypr3d-0.5.0.r67.g3656ac7-1.md and the
  reviews it names) plus three commits on the fork's branch larch/main:
  AfrobamaYT/Hypr3D `e078c4006f181182f62edaad13c3d73b2e98cab0`. The GitHub
  archive of that commit has SHA-256
  `a7f97cf27896ba53ecb488b27c578281b6a9f378de0d66c02f668c6231f075eb` ("Passed"
  in the build log).
- Why: the owner's PC has three monitors and the room covered one; he chose
  one room across all three (2026-10-06).
- The three commits, written in this session and read in full; none adds a
  file, process, network or library call, and none a thread:
  - `b04b8ba` (~350 lines): every enabled, non-mirroring monitor shows the room
    (`world.span`, default true) through its own off-axis window of one view
    plane -- Kooima's generalized perspective projection for a flat wall of
    screens, as CAVEs and triple-screen simulators use. A neighbour's pass only
    draws (`Mat4::frustum`); clock, physics, transition, HUD, crosshair and
    the probe stay with the target monitor. `GLScene` keeps one offscreen
    target per size (at most four), deleted in `shutdown()`. The windows of
    every spanned monitor are ghosted in one pass and captured on their own
    monitor; entering the room they become a wall where they stood. Leaving
    the room and `PLUGIN_EXIT` damage every monitor. Its pass element is still
    "Hypr3D", so `removeAllOfType` takes every monitor's.
  - `a4849b7`: a layer surface's box is in layout coordinates (Hyprland's
    `arrangeLayerArray` starts from the monitor's position); the room took it
    as monitor-local. Upstream's fault: on a monitor away from the origin a
    bar, a notification or a full-screen dialog sampled outside its snapshot.
  - `e078c40`: the wall's stacking step moves each item along its own sight
    line and only over what it overlaps; the status file lists each spanned
    monitor's items (kind, monitor, box, captured, in the world).
- The recipe at `e14bc70a` differs from r67's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d` in
  the clean chroot against hyprland 0.56.2-4; its `.BUILDINFO` records the
  committed PKGBUILD's SHA-256 `1f1e6c7a286f...`. The `-debug` package is not
  published. r68 (b04b8ba alone) was built and never approved: its acceptance
  found the two faults `a4849b7` and `e078c40` fix.
- Release VM (virgl, Hyprland 0.56.2-4), this exact archive installed with
  pacman, two headless outputs beside Virtual-1 -- the main monitor at
  x = 2560, the others left of and above it: the bars, notifications, a
  full-screen dialog and two terminals of all three monitors in the room
  where they stood, nothing cutting into anything; three rounds of load, on,
  unload while on: the same Hyprland PID, no coredump. Earlier with the same
  source built by cmake: the seams continue to the pixel (edges in the same
  layout rows on both sides), every monitor is the 2D desktop again after
  the room closes, one monitor keeps the arc, `world.span = false` keeps the
  one-monitor view.
- The owner's RTX 3080, this exact archive inside `larch-rice try --offscreen
  caelestia` with three headless outputs laid out like his desk (1920x1080 at
  0,0; 3840x2160 at scale 2 at 1920,45; 1920x1080 at 675,-1080): three rounds
  on/off, on, unload while on -- the nested Hyprland alive, no coredump; his
  session's PID, environment and monitors unchanged. The windows of the
  monitors are given as tangents in the status file and match the layout.
- Not measured: his real three-monitor session (only headless outputs in a
  nested compositor on his GPU); monitors with different pixel densities
  (the plane uses logical px, his three are within 2% of each other); tilted
  side screens and bezels, which are not modelled.
- License: MIT (Hypr3D, Jolt; both installed), stb_image and font8x8 public
  domain, cgltf MIT; libjpeg-turbo is linked, not included.
- Exact approved archive:
  `hypr3d-0.5.0.r70.ge078c40-1-x86_64.pkg.tar.zst`, SHA-256
  `57f0ec471839b08b1c4120dc7dc63293305fa8194d45e027b01b860927ca86cf`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r67.g3656ac7-1.
