# hypr3d 0.5.0.r100.g31512ed-1, x86_64

- What it is: 0.5.0.r99.g99cea05-1 (see hypr3d-0.5.0.r99.g99cea05-1.md and
  the reviews it names) plus one commit on the fork's branch larch/main,
  AfrobamaYT/Hypr3D `31512edcb77d1f7efeaf854925d904ecba2ffd9f`. The GitHub
  archive of 31512ed has SHA-256
  `55c169f76eb5504204dffd150cc17d9ccbce262c51276a05f73f5a6d7a1a9c13`
  and holds exactly that commit's tree (compared file by file against
  `git archive`).
- Why: on the owner's three monitors the room's view jumped to his top
  monitor whenever a window laid out there came under the crosshair (his
  status log: the view on DP-2 until t=560.9 s, on HDMI-A-1 from 561.2 s).
- The commit, written in this session and read in full: targetMonitor()
  returns the monitor the room was entered from while the room is open,
  held as a weak reference and used only while it is enabled; a configured
  monitor still wins. Bookkeeping only: no file, process, thread, library
  or network call is added.
- The recipe at `4248b0ce` differs from r99's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d`
  in the clean chroot against hyprland 0.56.2-4 (the source archive's
  checksum "Passed"); its `.BUILDINFO` records the committed PKGBUILD's
  SHA-256 `c0a9c2e69444...`, which matches. The `-debug` package is not
  published.
- Measured in `larch-rice try --offscreen caelestia` (nested Hyprland
  0.56.2-3 as the owner's PC runs it, on his RTX 3080) with this archive's
  `hypr3d.so` (SHA-256 `ad5e5b04f614...`): on his layout of three monitors
  (`.werkstatt/mondstation/tools/span/focus-drift.sh`), looking up onto the
  top monitor's terminal and right onto the 4K one's, the view stays on the
  main monitor in all 14 steps while the keyboard focus moves (r99 moved
  the view to the other monitor at the first window); in a fresh
  one-monitor sandbox the Backrooms TV test gives r99's results exactly
  (put on the TV 1724x1020, Super+wheel 1095x648, F8, Super+F 1920x1080 and
  back).
- Not measured: the owner's real session with this build.
- License: unchanged, MIT (Hypr3D, Jolt; both installed), stb_image and
  font8x8 public domain, cgltf MIT; libjpeg-turbo is linked, not included.
- Exact approved archive:
  `hypr3d-0.5.0.r100.g31512ed-1-x86_64.pkg.tar.zst`, SHA-256
  `1608b29b57177b43f1bf4fbbefc2eec553446e8c425ecdd4f4e3bca86c9436a0`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r99.g99cea05-1.
