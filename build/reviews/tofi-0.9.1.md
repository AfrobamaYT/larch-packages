# tofi 0.9.1-2, x86_64

- Provenance: philj56/tofi, tag `v0.9.1` on commit `71a4801d20d8`
  (2023-04-10), the newest release. The recipe's sha512 equals the download,
  and the unpacked tarball is identical to `git archive` of the tag.
- The local PKGBUILD is the AUR recipe at `0ee27a5` (2023-05-15), unchanged;
  its `check()` runs tofi's own tests.
- Capabilities (8,670 lines of C): a dmenu-style menu on a layer surface. It
  reads its choices from stdin (`tofi`), from PATH (`tofi-run`, which prints
  the choice for the caller to run) or from desktop entries (`tofi-drun`,
  which starts the chosen application through GIO's `g_app_info_launch` or
  prints it); it keeps its lists in `~/.cache/tofi-*`. No network, no shell of
  its own.
- Needed by: hyprdots, uwumdoescomputershit.
- Dependencies: freetype2, harfbuzz, cairo, pango, wayland, libxkbcommon,
  glib2 -- all in Arch's repositories.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable; the MIT
  text is installed.
- Release VM, 2026-09-30, installed from the image of that day with [larch]
  (fix proof p24): the wave's six archives installed with `pacman -U`;
  hyprdots and uwumdoescomputershit, which had stopped at this package,
  fetched complete and switched there and back, as did the rest of the wave's
  eight rices.
- License: MIT.
- Not done: greps for processes, files and network plus the code around every
  hit, not a line-by-line reading.
- Exact approved archive:
  `tofi-0.9.1-2-x86_64.pkg.tar.zst`, SHA-256
  `429d8bd2117a636e516cf7bb45c4bc48cd778bd1b14f41dbb021455254ef515a`.
  This approval covers no other version, architecture, or build.
