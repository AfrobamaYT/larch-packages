# hypr3d 0.5.0.r120.g91cbab6-1, x86_64

- What it is: 0.5.0.r119.g75a6714-1 (see hypr3d-0.5.0.r119.g75a6714-1.md
  and the reviews it names) plus one commit on the fork's branch larch/main,
  AfrobamaYT/Hypr3D `91cbab6ee6ad064d1142a505e05e6a3ccfe0bed5`. The GitHub
  archive of 91cbab6 has SHA-256
  `956548921f3579300b5ecf34ff7618fd5b098076aa5541c3889a04ee5d5aa5e8`
  and holds exactly that commit's tree (compared file by file against
  `git archive`).
- Why: on 2026-10-08 20:29 the owner's Hyprland (with r119 loaded) dumped
  core with SIGTRAP while he walked through the Backrooms, and
  start-hyprland brought it back in safe mode. The stack, symbolised with
  r119's debug package (same build ID f0d34b6a...), runs from update3D
  through Jolt's PhysicsSystem::Update and CollideConvexVsTriangles into
  `JPH_ASSERT(!ioV.IsNearZero())` (EPAPenetrationDepth.h:111): an assert,
  compiled in because the recipe's CMAKE_BUILD_TYPE=None sets no NDEBUG and
  Jolt then turns JPH_DEBUG and every assert on. Every earlier package had
  them; the sandbox's Release builds did not, which is why no test saw it.
- The commit, written in this session and read in full: the fork's
  CMakeLists defines Jolt's JPH_NO_DEBUG (Jolt's Build/README.md) on the
  Jolt target, public, for every configuration but Debug. Nothing else
  changes. Without the assert Jolt runs that GJK step as its release
  builds do.
- The recipe at `7d598182` differs from r119's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d`
  in the clean chroot against hyprland 0.56.2-4 (the source archive's
  checksum "Passed"); its `.BUILDINFO` records the committed PKGBUILD's
  SHA-256 `283db4e84187...`, which matches. The archive holds the .so and
  the two licences; `ldd` finds every library. The `-debug` package is not
  published.
- Measured on this archive's `hypr3d.so` (SHA-256 `14b487627cd1...`):
  the assert string `!ioV.IsNearZero()` 0 times (r119: 1), `int3`
  instructions 0 (r119: 2555). In `larch-rice try --offscreen caelestia`
  (nested Hyprland 0.56.2-4, the owner's RTX 3080): walking the Backrooms
  in five directions, stopping at its walls; the crosshair test's states as
  with r119.
- Not measured: the trap itself reproduced on demand -- it needs the
  degenerate contact the owner walked into.
- License: unchanged, MIT (Hypr3D, Jolt; both installed), stb_image public
  domain, cgltf MIT; libjpeg-turbo, cairo and pango are linked, not
  included.
- Exact approved archive:
  `hypr3d-0.5.0.r120.g91cbab6-1-x86_64.pkg.tar.zst`, SHA-256
  `196cd260ec736d46ce8248f64d82f68ea8c8abd7852e3964e08bf972f81197d7`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r119.g75a6714-1.
