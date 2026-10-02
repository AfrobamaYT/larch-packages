# aquamarine 0.15.1.1-1, x86_64

- What it is: Arch's extra/aquamarine 0.15.1-1 (archlinux/packaging @ 33bf60a,
  0BSD) with one upstream commit on top: hyprwm/aquamarine
  `fc77bd58a2c9ef6d0760a7c9c3b7b6670f956f28` "drm: fix crash on null connector
  in flush" (Vaxry, 2026-09-22), on `main` since then and in no release yet
  (0.15.1 of 2026-09-17 is the newest, checked 2026-10-02). The patch adds a
  null check to one condition in `CDRMBackend::flushAsyncCommitEvents`.
- Why: the greeter's Hyprland crashed at every login on the owner's NVIDIA
  desktop with more than one screen (SIGSEGV in that function, aquamarine
  #383; RELEASE-LUECKEN.md, measured 2026-09-29 and 2026-10-02). The owner
  chose the carry on 2026-10-02.
- Provenance: the v0.15.1 tarball's SHA-256 `2f9de98c...` equals Arch's
  recipe; the patch is GitHub's `.patch` of that commit, applied with
  `patch -Np1` (the build log says "patching file src/backend/drm/DRM.cpp").
- The recipe at `7628ba86` differs from Arch's only in the header, `pkgver`
  0.15.1.1 with `_upstreamver` 0.15.1 for the source, the patch in
  `source` and `prepare()`. 0.15.1.1 sorts after Arch's 0.15.1-N and before
  0.15.2, so the next Arch release replaces it on -Syu; [larch] stays last in
  pacman.conf, so it is installed by name (`larch/aquamarine`).
- The archive holds the same files as Arch's aquamarine 0.15.1-1 and provides
  the same `libaquamarine.so=14-64`, so Hyprland 0.56.2 links it unchanged.
  Built with `tools/larch-packages build aquamarine` in the clean chroot; its
  `.BUILDINFO` records the committed PKGBUILD's SHA-256 `ef04ea34...`. The
  `-debug` package the build also made is not published.
- Not measured: whether the crash is gone -- that needs a login on the owner's
  PC with this package installed. A comparison of the machine code with Arch's
  build says nothing either way: a different compiler inlined differently.
- License: BSD-3-Clause (LICENSE installed).
- Exact approved archive:
  `aquamarine-0.15.1.1-1-x86_64.pkg.tar.zst`, SHA-256
  `f9b1b6a339e3e80d84c55a8296aec11f44f389c233f91905b407adad7d194ca7`.
  This approval covers no other version or build.
