# hypr3d 0.5.0.r67.g3656ac7-1, x86_64

- What it is: 0.5.0.r61.gd681e3b-1 (see hypr3d-0.5.0.r61.gd681e3b-1.md and,
  for the vendored code, files and version check, hypr3d-0.5.0.r58.gd0be2e0-1.md)
  plus six commits on the fork's branch larch/main: AfrobamaYT/Hypr3D
  `3656ac75d05219a6b80a70cd15cb735894f5b903`. The GitHub archive of that
  commit has SHA-256 `499e9afecd8d080b10c0b2e32bdbd0b9db2bcb5ce895437b9d08753092eb4916`
  ("Passed" in the build log).
- The six commits, read in full (~600 lines in `MapModel`, `MapCollision`,
  `GLScene`, `main.cpp`, `CMakeLists.txt`); none adds a process, network or
  library call except libturbojpeg:
  - `54e1cb5`: the aim ray walks the collision tree by a slab test.
  - `bb4277a`, `6d040e3`, `46e28a4`: worker threads (`std::jthread`) read and
    decode scene models and cook a static model's Jolt `MeshShape`; GL objects
    are made on the render thread, one texture per frame. Workers call no GL.
    A result passes by an atomic flag stored with release and loaded with
    acquire, the thread joined before its data is read. `load()` and the model's
    destructor stop and join its worker; `joltShutdown()` joins every shape
    job. Both run in `PLUGIN_EXIT`, before Hyprland unmaps the code. Each worker
    catches every exception (one leaving a thread would terminate Hyprland).
    Physics stands still while a model is still loading. Cost noted: a reload
    or exit mid-decode waits on the render thread until the image being
    decoded is done.
  - `fc7b9bb`: Release when cmake gets no build type; this recipe passes
    `None` and is unchanged by it.
  - `3656ac7` (written in this session): an embedded image hyprgraphics cannot
    read (it reads PNG, AVIF and SVG from memory) is decoded as JPEG through
    libjpeg-turbo's TurboJPEG API when it starts FF D8 FF, with its limits for
    untrusted input set (500 progressive scans, 8192x8192 pixels, 512 MB).
    libjpeg-turbo 3.2.0 is already in the compositor through hyprgraphics; it
    is now a direct dependency of this package.
- Three `-Wstringop-overflow` warnings in the build come from unmodified Jolt
  5.2.0's `VehicleCollisionTester.cpp` (atomics inlined from `Body::IsSensor`);
  Hypr3D uses no vehicles.
- The recipe at `61fe0f84` differs from r61's in the header, `_commit`,
  `pkgver`, the checksum and `libjpeg-turbo` in `depends`. Built with
  `tools/larch-packages build hypr3d` in the clean chroot against hyprland
  0.56.2-4; its `.BUILDINFO` records the committed PKGBUILD's SHA-256
  `0a9f2a135892...`. The `-debug` package the build also made is not
  published.
- Release VM (virgl, Hyprland 0.56.2-4), a fresh overlay, this exact archive
  installed with pacman, hypridle stopped:
  - unloading while the room is shown: 5 of 5 without a crash;
  - unloading while a 47 MB model (Khronos FlightHelmet, CC0) decodes, page
    cache dropped first: 3 of 3 without a crash;
  - the longest `hyprctl version` round trip, probed every 50 ms while
    FlightHelmet comes into the open room: r61 331 ms, this archive 22 ms;
  - Super+Shift+F12 through `larch-3d` loads it and enters the room, the
    second press leaves; the same Hyprland PID and no coredump through all
    of it; three terminals stand side by side on the arc.
  - Embedded JPEGs, measured with the plugin built from `fc7b9bb` and from
    `3656ac7`: DamagedHelmet.glb (Khronos, CC BY 4.0, five embedded JPEGs)
    black before; after, its emissive texture shows, and a copy without the
    emissive texture shows the full base colour. With an emissive texture
    the map shader draws emissive instead of the lit base colour --
    upstream's rule for baked Sketchfab rooms, not a decoding fault -- so the
    original helmet stays dark outside its glowing parts.
- Not measured: real hardware (AMD, Intel, NVIDIA).
- License: MIT (Hypr3D, Jolt; both installed), stb_image and font8x8 public
  domain, cgltf MIT; libjpeg-turbo is linked, not included.
- Exact approved archive:
  `hypr3d-0.5.0.r67.g3656ac7-1-x86_64.pkg.tar.zst`, SHA-256
  `7b00e5f1605593ca2d537c5199d912e73e2f5bb2cfbc21251186cd0b4535c107`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r61.gd681e3b-1.
