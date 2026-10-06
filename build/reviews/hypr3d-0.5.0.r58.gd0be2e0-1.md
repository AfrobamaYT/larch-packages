# hypr3d 0.5.0.r58.gd0be2e0-1, x86_64

- What it is: Hypr3D (samine825/Hypr3D, MIT), a Hyprland plugin that draws the
  session as a walkable 3D room. Commit `d0be2e0b99b02c5689f4821eaf9eff6bf1690521`
  (2026-10-05), version string 0.5.0, 58 commits. The GitHub archive of that
  commit has SHA-256 `6625d5d8e934336ef007fdd17d7d31093735a9fc9a9ac1e29f45ed56294c0b45`
  ("Passed" in the build log).
- The recipe at `6eed133f` installs `/usr/lib/hyprland/hypr3d.so` and two
  licence files, nothing else. Built with `tools/larch-packages build hypr3d`
  in the clean chroot against hyprland 0.56.2-4, aquamarine 0.15.1.1-2,
  hyprutils 0.14.2-1, hyprgraphics 0.5.1-4, hyprcursor 0.1.13-7, hyprlang
  0.6.8-5; its `.BUILDINFO` records the committed PKGBUILD's SHA-256
  `4094863d6cc5...`. The `-debug` package the build also made is not
  published.
- Vendored code, compared byte for byte with upstream on 2026-10-06:
  `third_party/Jolt` is JoltPhysics v5.2.0 with no differing file;
  `stb_image.h` is stb master (v2.30); `cgltf.h` is jkuhlmann/cgltf master
  (its header still says 1.15). `font8x8_basic.h` (public domain) differs
  from its original only in `const unsigned char`.
- The plugin's own code (14,902 lines under `src/`), searched for every way
  out of the compositor: no process start (`system`, `popen`, `exec*`,
  `fork`, `posix_spawn`), no socket, no `dlopen`/`dlsym`, no `setenv`. It
  registers three dispatchers (`hypr3d:toggle|open|close`) and Lua functions
  under `hl.plugin.hypr3d`, and hooks one Hyprland function on the pointer
  path, found by name (`HyprlandCompat/PointerHook.cpp`).
- Files it touches: reads the glTF scenes, player model and panorama the
  person's config names (`~` expanded from `$HOME`), parsed in the compositor
  by cgltf and stb_image -- a model from an untrusted source is untrusted
  code input to the compositor. Larch's config names none. Writes
  `/tmp/hypr3d-status.txt` (appended about four times a second while the room
  is shown, cut back at 128 KiB) and `/tmp/hypr3d-skirt-mask.pgm` (once per
  load): fixed names in the shared `/tmp`; with systemd's default
  `fs.protected_regular=1` another user can block these diagnostic writes but
  not redirect them.
- Version check: `PLUGIN_INIT` compares `__hyprland_api_get_hash()` with the
  hash it was built with (Hyprland commit plus the major.minor of aquamarine,
  hyprutils, hyprgraphics, hyprcursor, hyprlang) and throws on a mismatch.
  Measured with a build whose `GIT_COMMIT_HASH` was zeroed: "plugin
  crashed/threw in main: [hypr3d] Hyprland API hash mismatch", Hyprland
  unharmed. `hyprctl plugin load` exits 0 on that failure, so `larch-3d`
  checks its output and shows the reason.
- Release VM (virgl, Hyprland 0.56.2-4, Arch's aquamarine 0.15.1-1) with this
  exact archive: Super+F12 by real key input loads the plugin (155 ms with
  the host build) and shows the windows as separate panels over the grid
  floor; Super+F12 inside the room returns to the desktop; logging out with
  `uwsm stop` from inside the room ends without a crash. Hyprland's resident
  memory 158.5 MB before, 162.6 MB in the room, 162.8 MB back on the desktop.
- ⛔ Measured fault, upstream's: `hyprctl plugin unload` while the room is
  shown crashes Hyprland (SIGSEGV, two of two; the watchdog restarts it in
  safe mode). The backtrace calls from `IHyprRenderer::beginRender` into the
  unmapped plugin, consistent with a `CHypr3DPassElement` left in the render
  pass. Unloading on the desktop: no crash (one of one). Nothing in Larch
  unloads it: `larch-3d` loads it outside the config, and Hyprland unloads
  only plugins its config named.
- Not measured: real hardware (AMD, Intel, NVIDIA); a scene or player model.
- License: MIT (Hypr3D, Jolt; both installed), stb_image and font8x8 public
  domain, cgltf MIT.
- Exact approved archive:
  `hypr3d-0.5.0.r58.gd0be2e0-1-x86_64.pkg.tar.zst`, SHA-256
  `dc8899ebd6bfddff97a37c1baa99e13dfd65235acfce637cb29aa95159f54798`.
  This approval covers no other version or build.
