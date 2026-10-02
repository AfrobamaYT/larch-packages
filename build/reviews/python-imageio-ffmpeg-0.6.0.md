# python-imageio-ffmpeg 0.6.0-2, any

- Provenance:
  - Tag `v0.6.0` is a lightweight tag on the unsigned commit
    `ae47d8028c237ca5507ceef1b843ee427b442887`.
  - The recipe's sha256 equals the download, and the unpacked tarball equals
    `git archive` of the tag. PyPI's sdist (matching PyPI's digest) has the
    same code plus `PKG-INFO`, `setup.cfg` and egg-info.
- The local PKGBUILD is the AUR recipe at `c9adcba` (2026-04-19), unchanged.
  It builds with setuptools' legacy backend (`--no-isolation`); upstream's
  `setup.py` only reads the version from `_definitions.py`. Nothing is
  downloaded.
- No bundled ffmpeg: `imageio_ffmpeg/binaries/` holds only `README.md` and
  `__init__.py` in the tag and in this archive. PyPI's platform wheels carry
  a static ffmpeg; this package is built from the source tag, never from a
  wheel, and depends on Arch's `ffmpeg`.
- Which ffmpeg it runs (`_utils.py:13-62`): `IMAGEIO_FFMPEG_EXE` if set,
  unchecked; a bundled binary (absent); `sys.prefix/bin/ffmpeg`, i.e.
  `/usr/bin/ffmpeg`; `ffmpeg` from `PATH`. The last two are validated with
  `ffmpeg -version`.
- Capabilities: it starts only ffmpeg, as argument lists without a shell,
  with the input path as its own argument. No network, no privilege, no file
  writes except `write_frames` to a caller-given path (waypaper only reads).
  Arch's ffmpeg parses untrusted wallpaper videos when waypaper makes
  thumbnails.
- Needed by waypaper for video thumbnails.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; the archive's `.BUILDINFO` records the sha256
  of this PKGBUILD. The file list matches the recipe: the Python package
  under `/usr/lib/python3.14/site-packages` and the license. No file is
  setuid or group-writable.
- Release VM, 2026-09-30: installed with `pacman -U` beside the other eight
  packages of this set and caelestia's six; `get_ffmpeg_exe()` returned
  `/usr/bin/ffmpeg`.
- License: BSD-2-Clause, installed.
- Not done: Arch's ffmpeg itself, including how it treats playlists or URLs
  inside local media files.
- Exact approved archive:
  `python-imageio-ffmpeg-0.6.0-2-any.pkg.tar.zst`, SHA-256
  `0575420dc77864a6399ef8834d33cf206a01d8ca20edb6b70e1fc06c1809342a`.
  This approval covers no other version, architecture, or build.
