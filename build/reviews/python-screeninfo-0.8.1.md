# python-screeninfo 0.8.1-2, any

- Provenance:
  - The recipe's URL resolves to tag `0.8.1`, a lightweight tag on
    `0cf3055ccaf583a00a7a3a049f85a7c58dfd8884`. That commit is PGP-signed;
    `git verify-commit` gives a good signature from
    `DEA244FD0BE4151466C73583CC65E6FD28CAE42A`, a key available only from
    github.com/rr-.gpg (keyserver.ubuntu.com answers 404).
  - The recipe's sha256 equals the download, and the unpacked tarball is
    byte-identical to `git archive` of the tag. PyPI's sdist for 0.8.1
    (matching PyPI's digest) has the same files plus `PKG-INFO` and a
    generated `setup.py`.
- The local PKGBUILD is the AUR recipe at `358c408` (2026-05-07), unchanged.
  It builds a wheel with poetry-core (`--no-isolation`, from [extra]) and
  installs it with the license; nothing is downloaded and no upstream code
  runs at build time.
- Capabilities: none beyond reading monitor geometry.
  - No network, no file writes, no privilege, no telemetry; importing it has
    no side effects.
  - `get_monitors()` tries Windows, Cygwin, Xrandr, Xinerama, DRM and OSX
    enumerators in order. The Cygwin one calls `dlopen("user32.dll")` even
    on Linux, which fails harmlessly unless `LD_LIBRARY_PATH` holds an empty
    entry (then the current directory is searched).
  - It loads libX11, libXrandr, libXinerama and libdrm through
    `ctypes.util.find_library`, which runs `/sbin/ldconfig -p` and, for a
    library missing from the cache, `gcc`/`ld`/`objdump` from `PATH`.
  - The DRM fallback opens `/dev/dri/card0..15` read-only to query modes.
- Needed by waypaper, which imports it unconditionally.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; the archive's `.BUILDINFO` records the sha256
  of this PKGBUILD. The file list matches the recipe: the Python package
  under `/usr/lib/python3.14/site-packages` and the license. No file is
  setuid or group-writable.
- Release VM, 2026-09-30: installed with `pacman -U` beside the other eight
  packages of this set and caelestia's six; `get_monitors()` returned the VM's
  monitor `Virtual-1`.
- License: the installed `LICENSE.md` holds MIT (Marcin Kurczewski) and
  BSD-3-Clause for the DRM driver (The Chromium OS Authors); the recipe's
  `license` field names only MIT.
- Not done: drm.py's ctypes memory handling; the four unreleased commits
  after the tag.
- Exact approved archive:
  `python-screeninfo-0.8.1-2-any.pkg.tar.zst`, SHA-256
  `4143d6a92d957ce6487595006f7ba38b3020e4d7b22c798d88521ae4e000bae1`.
  This approval covers no other version, architecture, or build.
