# hypr3d 0.5.0.r84.g61bda92-1, x86_64

- What it is: 0.5.0.r82.g90a21d9-1 (see hypr3d-0.5.0.r82.g90a21d9-1.md and
  the reviews it names) plus two commits on the fork's branch larch/main,
  AfrobamaYT/Hypr3D `c3e6d81` and `61bda92fc6107f8d277ef98bedddccc499195cf7`.
  The GitHub archive of 61bda92 has SHA-256
  `5455ebc13b469dbb6835a78b9eeeb28f879034e40a959ed3fe18ce0bde7ca762`
  and holds exactly that commit's tree (compared file by file against
  `git archive`).
- Why: the two points r82's review left open -- the room's picture of a
  window was not the window's own (95 % of the pixels), and the cinema key
  from the owner's idea report.
- The commits, written in this session and read in full:
  - `c3e6d81`: the composite shader that puts the scene over Hyprland's
    frame declares `highp` instead of `mediump`. It flips v as
    `1.0 - vUV.y`, and the RTX 3080 runs mediump arithmetic as 16-bit
    floats: rows were sampled on a sawtooth up to 0.4 of a row off.
  - `61bda92`: F4 brings the aimed window to the eye as F2 does, scaled to
    90 % of the view, and darkens the rest of the room to a fifth of its
    light; the featured window is drawn last without the depth test, after
    a black quad of that alpha. The companion's eye ignores both.
  - No file, process, thread, library or network call is added.
- The recipe at `f727e545` differs from r82's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d` in
  the clean chroot against hyprland 0.56.2-4 (the source archive's checksum
  "Passed"); its `.BUILDINFO` records the committed PKGBUILD's SHA-256
  `9409191ebcb3...`, which matches. The `-debug` package is not published.
- Measured in `larch-rice try --offscreen caelestia` (nested Hyprland 0.56.2
  on the owner's RTX 3080), a foot terminal of 960x540 floating at
  480,270, read with F2 against the same window in 2D:
  - with a diagnostic build: the snapshot framebuffer matched 2D 99.95 %
    (the rest the pointer), the scene framebuffer matched the snapshot
    100.00 %, the screen matched the scene 94.70 % -- the composite;
  - after `c3e6d81`: the screen matches the 2D window 100.00 %, max 0;
  - F4 on the Moon station: the terminal at 1622x895, the floor below it
    at 20 % of its brightness; F2 from there 960x540 again at 100 %; F4
    and F4 back to the wall; the companion's picture not dimmed.
  - This exact archive's `hypr3d.so` (SHA-256 `4cb2086387a8...`) on
    hyprland 0.56.2-3 as the owner's PC runs it: F2 matched the 2D window
    100.00 % with max difference 0; F4 showed the window big and the room
    dark (a corner of the view 5.3 -> 1.3); locked, `open()` printed
    "hypr3d: the session is locked" and the lock screen showed.
- Not measured: the owner's real session and its three monitors with this
  build; other GPUs' mediump in the shaders that pass texture coordinates
  through without arithmetic (exact on this GPU).
- License: unchanged, MIT (Hypr3D, Jolt; both installed), stb_image and
  font8x8 public domain, cgltf MIT; libjpeg-turbo is linked, not included.
- Exact approved archive:
  `hypr3d-0.5.0.r84.g61bda92-1-x86_64.pkg.tar.zst`, SHA-256
  `a92de55c8617c3757c0b90b53516b0cf233a5f21f0a641e3a64518950461c426`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r82.g90a21d9-1.
