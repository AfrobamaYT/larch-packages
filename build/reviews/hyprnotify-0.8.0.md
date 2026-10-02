# hyprnotify 0.8.0-1, x86_64

- Provenance: codelif/hyprnotify tag `v0.8.0` on commit `45d5ebd416bf`
  (2024-09-30); the recipe's sha256 equals the download, and the unpacked
  tarball is identical to `git archive` of the tag.
- The local PKGBUILD is the AUR recipe at `27d04e3` (2024-09-30), unchanged;
  Go modules come from go.sum.
- Capabilities (532 lines of Go): a notification daemon (it owns
  `org.freedesktop.Notifications` when started) that shows each notification
  with Hyprland's own `notify` over its IPC socket in the runtime directory
  (the pre-0.40 `/tmp/hypr` path only as a fallback); no processes, no
  network.
- Needed by: iamghost755-hyprdots.
- Dependencies: none at run time.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: Apache-2.0.
- Not done: greps for processes, files, sockets and network plus the code
  around every hit, not a line-by-line reading.
- Release VM, 2026-09-30, image of that day with [larch] (base 033fc7cc, proof
  run p26 on release VM 1): installed with `pacman -U`; iamghost755-hyprdots
  fetched complete and switched there and back.
- Exact approved archive:
  `hyprnotify-0.8.0-1-x86_64.pkg.tar.zst`, SHA-256
  `720929a9466211dfae0f3869b8c3d87f31dc8ca9f0131f0f65f9ad99665ae7be`.
  This approval covers no other version, architecture, or build.
