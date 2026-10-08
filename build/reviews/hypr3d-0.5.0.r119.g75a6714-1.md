# hypr3d 0.5.0.r119.g75a6714-1, x86_64

- What it is: 0.5.0.r103.gc1f3ec4-1 (see hypr3d-0.5.0.r103.gc1f3ec4-1.md and
  the reviews it names) plus sixteen commits on the fork's branch
  larch/main, AfrobamaYT/Hypr3D `75a67143450259ff2f3e3f9b18e52923ce8833be`.
  The GitHub archive of 75a6714 has SHA-256
  `6bdfcfbd5df3752da6423e0aa589fed172966835363729c8e0c7834d737b0309`
  and holds exactly that commit's tree (compared file by file against
  `git archive`).
- Why: the owner approved four Claude Design drafts for the room on
  2026-10-08 ("Ja Passt alles") -- room overlays, room motion, portals and
  the menu's sections -- and asked for them built.
- The commits, all written in this session and read in full:
  c20ebc2, d160a33, 2a0fc09 (Super+F twice stays in the room, the F1 menu
  and Super+F used from the start, an arrow pointer), 03babe6, 18e9916,
  0e0db98 (windows("reset"/"undo"); flying, gravity and HUD written to
  `$XDG_RUNTIME_DIR/hypr/$SIG/hypr3d-state` for the menu), 19bb9a6 (a
  window carried to the bin crumples into a paper ball), 4fad617, 182a229,
  8867914, d2b744a (the crosshair's marks and labels, Larch's pointer, F3 as
  a panel, the bin's note -- drawn with Cairo and Pango into textures),
  f49bb34, fc2cf50 (F2, Super+F and the menu on the drafts' curves; the
  room dimmed, and blurred behind the menu by a dual Kawase pass), 72fdd43
  (the windows lift off their 2D tiles into the room and back over the
  captured wallpaper; a transition step is at most 50 ms), 21cd50b,
  75a6714 (portals as lit doors with a plate and focus; going through:
  the cover to the screen, a starting panel fed by the new
  `hl.plugin.hypr3d.portal_state`, Esc and Enter).
- What changed at the edges: the plugin now links cairo and pango (system
  libraries, declared in depends) and reads the system's fonts through
  fontconfig. It captures the monitor's background layer (the wallpaper)
  while the room is open, as it captures every other layer. Enter on a
  failed portal start runs the portal's command again through Hyprland's
  executor, as walking into it already did. portal_state only changes what
  the panel shows, a portal's note, and where the player stands. No file is
  written beyond hypr3d-state, no process, thread or network call is added;
  the font8x8 bitmap font is gone.
- The recipe at `931c0f6d` differs from r103's in the header, `_commit`,
  `pkgver`, the checksum and `cairo`, `pango` in depends. Built with
  `tools/larch-packages build hypr3d` in the clean chroot against hyprland
  0.56.2-4 (the source archive's checksum "Passed"); its `.BUILDINFO`
  records the committed PKGBUILD's SHA-256 `654dd1bc58dc...`, which
  matches. The archive holds the .so and the two licences; `ldd` finds every
  library. The `-debug` package is not published.
- Measured in `larch-rice try --offscreen caelestia` (nested Hyprland
  0.56.2-4 as the owner's PC runs it, on his RTX 3080) with this archive's
  `hypr3d.so` (SHA-256 `4f4b980e24ec...`), rigs in
  `.werkstatt/mondstation/tools/ui/`:
  - `aim-test.sh`: the ten crosshair states (sky, window first aim, label
    at 500 ms, folded at 2.7 s, the bin, carrying over the bin and off it,
    the gun on a window, holding, on the sky) as the status file and the
    frames show them.
  - `flight-test.sh`: into the room the three windows start on their 2D
    tiles and land where r103 puts them; out, back on the tiles, the
    desktop as it was.
  - `portal-run-test.sh` with a stand-in starter: the dive, the starting
    panel through four steps, the game's window ending it, and the player
    two steps in front of the portal when it quit. Earlier builds of the
    same commits: the failure panel with Esc, F2/Super+F dims 0.45/0.40,
    the menu's room clearing over 320 ms.
- Not measured: the owner's real session with this build; a real Steam
  start through a portal (Larch's larch-games launch was checked against
  a fake Steam directory only).
- License: unchanged, MIT (Hypr3D, Jolt; both installed), stb_image public
  domain, cgltf MIT; libjpeg-turbo, cairo and pango are linked, not
  included.
- Exact approved archive:
  `hypr3d-0.5.0.r119.g75a6714-1-x86_64.pkg.tar.zst`, SHA-256
  `04da08b41bd1c1f8411672e91e9f6ee0a74cce0347286cebfad96568627783ac`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r103.gc1f3ec4-1.
