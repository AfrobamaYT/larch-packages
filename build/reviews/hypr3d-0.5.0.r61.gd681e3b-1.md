# hypr3d 0.5.0.r61.gd681e3b-1, x86_64

- What it is: 0.5.0.r58.gd0be2e0-1 (see hypr3d-0.5.0.r58.gd0be2e0-1.md, whose
  findings on the vendored code, files, hooks and version check still hold)
  built from Larch's fork instead of upstream, the owner's decision of
  2026-10-06: AfrobamaYT/Hypr3D, branch larch/main, commit
  `d681e3b2cd3890979a941b1754b1db76aa199f8f`. The GitHub archive of that
  commit has SHA-256 `c49358aa8802ebef0abff7e4025535e8e48aec851ceeb42c37afad299e908cff`
  ("Passed" in the build log).
- The fork is upstream `d0be2e0` (an ancestor) plus three commits, 61 lines in
  `CMakeLists.txt` and `src/main.cpp`, read in full; none adds a file,
  process, network or library call:
  - `7069d1e` compiles every target with `-fno-gnu-unique`.
  - `1bfdbd3` places windows new to the room side by side on an arc around
    the camera, in their 2D order, instead of all at one spawn point.
  - `d681e3b` calls `g_pHyprRenderer->m_renderPass.removeAllOfType("Hypr3D")`
    first in `PLUGIN_EXIT`. The plugin's pass element names itself "Hypr3D"
    (`passName()`); `CRenderPass::removeAllOfType` erases by that name and is
    exported by Hyprland 0.56.2 (`nm -D`).
- The recipe at `0f6b20dd` differs from 0.5.0.r58's in the header, `_commit`,
  `pkgver` and the source URL and checksum. Built with `tools/larch-packages
  build hypr3d` in the clean chroot against hyprland 0.56.2-4; its
  `.BUILDINFO` records the committed PKGBUILD's SHA-256 `4698beac08f5...`.
  The `-debug` package the build also made is not published.
- `-fno-gnu-unique` changes nothing in this package: the chroot builds of
  both versions export 0 `STB_GNU_UNIQUE` symbols (makepkg's flags, LTO among
  them); a plain `cmake` Release build of upstream exports 75. In the release
  VM the reload path that crashed the fork's author's build -- load, room on,
  off, unload, load, room on -- did not crash with 0.5.0.r58 either (1 of 1).
  Kept: it holds for builds made with other flags.
- Release VM (virgl, Hyprland 0.56.2-4), red then green, a fresh overlay
  each:
  - 0.5.0.r58: unloading while the room is shown crashed Hyprland in round 2
    of 2 (earlier that day 2 of 2; 3 of 4 together).
  - this archive: reload path no crash; unloading while the room is shown,
    8 of 8 rounds without a crash -- the same Hyprland PID, no coredump, all
    three windows back on the desktop.
  - three terminals and Larch's look chooser in the room: side by side on an
    arc, not one panel in front of the others.
- Not measured: real hardware (AMD, Intel, NVIDIA); a scene or player model.
- License: MIT (Hypr3D, Jolt; both installed), stb_image and font8x8 public
  domain, cgltf MIT.
- Exact approved archive:
  `hypr3d-0.5.0.r61.gd681e3b-1-x86_64.pkg.tar.zst`, SHA-256
  `68c43fe54331960e037c934e62e90e91d2d56e6339f38a6f0113bd7a978f626f`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r58.gd0be2e0-1.
