# hypr3d 0.5.0.r103.gc1f3ec4-1, x86_64

- What it is: 0.5.0.r102.g82ed203-1 (see hypr3d-0.5.0.r102.g82ed203-1.md and
  the reviews it names) plus one commit on the fork's branch larch/main,
  AfrobamaYT/Hypr3D `c1f3ec494feff007738493fc249dc6500460cd8f`. The GitHub
  archive of c1f3ec4 has SHA-256
  `2eb2ab68cad7a1679fadcd338e46cca9b6682714b3e7940668ea5c90173ada80`
  and holds exactly that commit's tree (compared file by file against
  `git archive`).
- Why: the owner wanted Super+F in the room to show the window big in
  front of him with the room still around it, as Quest 3 does, with his
  mouse and keyboard on it -- not the 2D fullscreen it gave.
- The commit, written in this session and read in full: the room takes
  Super+F itself and puts the aimed window on a screen at 82% of the view
  (the cinema pose without the dimming), in F8's use mode from the start;
  Super+F again sends it back. A key's release now goes where its press
  went (a list of key codes whose press the room kept), and input the room
  takes while Super is held calls Hyprland's own shadowKeybinds, so no
  bind on releasing Super fires. No file, process, thread, library or
  network call is added.
- The recipe at `b25862ef` differs from r102's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d`
  in the clean chroot against hyprland 0.56.2-4 (the source archive's
  checksum "Passed"); its `.BUILDINFO` records the committed PKGBUILD's
  SHA-256 `bebcfea14578...`, which matches. The `-debug` package is not
  published.
- Measured in `larch-rice try --offscreen caelestia` (nested Hyprland
  0.56.2-4 as the owner's PC runs it, on his RTX 3080) with this archive's
  `hypr3d.so` (SHA-256 `33288cd36224...`):
  - `.werkstatt/mondstation/tools/screen/test.sh`: Super+F gives no
    Hyprland fullscreen, the window on the screen and in use; the mouse
    moves its pointer, the camera stays; "wasd hi" typed reaches the
    terminal whole and caelestia's launcher stays shut (with r102's key
    handling it opened and took the text); Super+F again sends it back and
    the mouse turns the camera.
  - `span/layout-leak.sh`, the owner's three monitors, nine visits: all
    clean but the expected new tile.
  - the Backrooms TV test: put on the TV, Super+wheel, F8 as before;
    Super+F now the screen instead of the 2D fullscreen.
- Not measured: the owner's real session with this build.
- License: unchanged, MIT (Hypr3D, Jolt; both installed), stb_image and
  font8x8 public domain, cgltf MIT; libjpeg-turbo is linked, not included.
- Exact approved archive:
  `hypr3d-0.5.0.r103.gc1f3ec4-1-x86_64.pkg.tar.zst`, SHA-256
  `c126f463af9e59de3f7c9ecc000ff6fb76e907054f979822cd773af34a0be602`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r102.g82ed203-1.
