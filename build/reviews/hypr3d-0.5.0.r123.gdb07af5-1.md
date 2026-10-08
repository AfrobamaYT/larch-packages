# hypr3d 0.5.0.r123.gdb07af5-1, x86_64

- What it is: 0.5.0.r122.g205fe59-1 (see hypr3d-0.5.0.r122.g205fe59-1.md
  and the reviews it names) plus one commit on the fork's branch larch/main,
  AfrobamaYT/Hypr3D `db07af507a55874a2a69bfa3f4c6cdd68374ca06`. The GitHub
  archive of db07af5 has SHA-256
  `0db9a0e3506e9d4017b121b5caa79a14499b2120ba4360b3dbf6fd7c428bccfb`
  and holds exactly that commit's tree (compared file by file against
  `git archive`).
- Why: on 2026-10-08 23:52 the owner's Hyprland (r122 loaded) dumped core
  as he left the room, and came back in safe mode. The stack, symbolised
  with r122's debug package: SIGSEGV in CWorkspace::isVisible, from
  CWindow::moveToWorkspace, from CWindowTarget::assignToSpace, from the
  plugin's restoreWindowLayout. The window restored was a 147x198 Steam
  window, alive but unmapped -- Hyprland resets a window's workspace on
  unmap and moveToWorkspace calls isVisible on the old one unchecked.
- The commit, written in this session and read in full: a window without a
  workspace only leaves the room's ghost (assignToSpace with no space,
  which touches no workspace) and gets its floating flag back. Nothing
  else changes.
- The recipe at `72a7644e` differs from r122's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d`
  in the clean chroot against hyprland 0.56.2-4; its `.BUILDINFO` records
  the committed PKGBUILD's SHA-256 `e5baa25ee581...`, which matches. The
  archive holds the .so and the two licences; `ldd` finds every library.
  The `-debug` package is not published.
- Measured on this archive's `hypr3d.so` (SHA-256 `36b084072271...`):
  `int3` instructions 0. In `larch-rice try --offscreen caelestia`
  (span/unmap-crash.sh: a GTK 3 window on XWayland hides itself while the
  room is open, then the room is left): r122's plugin aborts the sandbox's
  Hyprland with the owner's stack at the same offsets; this one survives,
  and the window shown again is a tile on its workspace. fs-leak.sh, the
  layout suite and the resize states give r122's results.
- License: unchanged, MIT (Hypr3D, Jolt; both installed), stb_image public
  domain, cgltf MIT; libjpeg-turbo, cairo and pango are linked, not
  included.
- Exact approved archive:
  `hypr3d-0.5.0.r123.gdb07af5-1-x86_64.pkg.tar.zst`, SHA-256
  `df600675ba25a5bb1ba96ec2033c93a4f14ab11a39fe11737ae0c8195291b5a1`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r122.g205fe59-1.
