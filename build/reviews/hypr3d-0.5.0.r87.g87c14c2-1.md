# hypr3d 0.5.0.r87.g87c14c2-1, x86_64

- What it is: 0.5.0.r86.g6d9ea79-1 (see hypr3d-0.5.0.r86.g6d9ea79-1.md and
  the reviews it names) plus one commit on the fork's branch larch/main,
  AfrobamaYT/Hypr3D `87c14c28106367117766bb6899804b0f7c829d28`. The GitHub
  archive of 87c14c2 has SHA-256
  `b14036d21e172791d1b4054103e498a36a2fc139af2735150fccf344e89365ed`
  and holds exactly that commit's tree (compared file by file against
  `git archive`).
- Why: the owner opened the room on his three monitors and the wall stood
  in the right arrangement but too low -- its lower third under the Moon
  station's deck (his screenshot, 2026-10-07).
- The commit, written in this session and read in full: as the wall of
  several monitors is built (an empty room), its scale is capped where its
  lowest monitor ends 5 cm above the player's feet, kept until reset();
  walking, the spawn's view is level. Arithmetic on the layout only: no
  file, process, thread, library or network call is added.
- The recipe at `9864db85` differs from r86's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d` in
  the clean chroot against hyprland 0.56.2-4 (the source archive's checksum
  "Passed"); its `.BUILDINFO` records the committed PKGBUILD's SHA-256
  `0d6779fc9e62...`, which matches. The `-debug` package is not published.
- Measured in `larch-rice try --offscreen caelestia` (nested Hyprland 0.56.2
  on the owner's RTX 3080) with his layout -- 1920x1080 at 0,0; 3840x2160 at
  scale 2 at 1920,45; 1920x1080 at 675,-1080 -- a terminal on each, walking
  on the Moon station: the share of each output's pixels that still look
  like its 2D desktop right after opening (within 24 levels), r86 -> this
  archive's `hypr3d.so` (SHA-256 `f2f53efa1c67...`, on hyprland 0.56.2-3 as
  his PC runs it): main 62 % -> 80 % (its lower quarter 28 % -> 83 %), right
  63 % -> 86 % (21 % -> 88 %), top 88 % -> 90 %. The rest is caelestia's
  wallpaper layer, which the room draws see-through, before as after. The
  wall stands 2.3 m off instead of 4.2 m.
- Not measured: the owner's real session with this build.
- License: unchanged, MIT (Hypr3D, Jolt; both installed), stb_image and
  font8x8 public domain, cgltf MIT; libjpeg-turbo is linked, not included.
- Exact approved archive:
  `hypr3d-0.5.0.r87.g87c14c2-1-x86_64.pkg.tar.zst`, SHA-256
  `379390ed8809e19a624dde4ca8d78386a843ae9617a4a558132015a5f8505a5d`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r86.g6d9ea79-1.
