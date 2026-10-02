# python-pywal16 3.8.15-1, any

- Provenance:
  - Upstream tag `3.8.15` is an annotated, unsigned tag on the unsigned
    commit `a04c3e3b57ec57bdf080a863f45f917a18208e58` (2026-04-10), the newest
    release.
  - The recipe's sha256 equals the download
    (`cd3e4588c453b844dd222d861b52b7a7c88a3396b3e104300ef1db27b9492b1d`), and
    the unpacked tarball is identical to `git archive` of the tag (371 files,
    4356 lines of Python).
- The local PKGBUILD is the AUR recipe at `d391e2c` (2026-04-11), unchanged.
  It deletes the schemer2 backend (no licence), builds with
  `python setup.py build` and installs with `setup.py install`; nothing is
  downloaded during the build. `setup.py` only reads the version and README.
- Capabilities:
  - Terminal colours: writes escape sequences to every `/dev/pts/*` the
    person can open (`sequences.py:send`), as pywal always did, and runs
    `sh ~/.cache/wal/colors-tty.sh` only on a Linux console (`TERM=linux`).
  - Processes, all with argument lists: `xrdb -merge`, `i3-msg reload`, `bspc
    wm -r`, `kitty @ set-colors` (inside kitty through its own terminal,
    otherwise `--to unix:/tmp/kitty_pywal`), wallpaper setters (`swww
    img`/`awww img`, `swaybg` after `killall swaybg`, `wbg` after `killall
    wbg`, feh and the X setters), `magick`/`convert` for the palette, `pidof`.
    `shell=True` occurs once, for OpenBSD's tty list with a fixed command.
  - `wal -o CMD` runs a command the person names, detached and without a
    shell.
  - Templates (`~/.config/wal/templates`, which rices ship): markers are
    parsed by a grammar whose names start with a letter and whose arguments
    are numbers only (`export.py:Parser`), resolved with `getattr` on the
    colour object. No dunder attribute, no string argument, so a template
    cannot reach code; it only formats colours.
  - Writes `~/.cache/wal/` (schemes, colours, exported templates); `wal -c`
    deletes `~/.cache/wal/schemes`. No network, no privilege, no telemetry
    (`donation.py` only prints a URL).
- Dependencies: all in Arch's repositories (imagemagick, procps, python, sh).
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD, and the archive holds `/usr/bin/wal`, the `pywal` package with its
  colour schemes and templates, and the license (401 files); the schemer2
  backend is gone. No file is setuid or group-writable.
- Release VM, 2026-09-30 (fix proof p10): installed with `pacman -U` together
  with the other archives staged for the sweep. raidontpaizer and lierb, which
  had stopped at this package, fetched complete -- the importer rendered
  raidontpaizer's Pywal assets with it ("generated 8 private Pywal asset(s)")
  -- and switched there and back.
- License: MIT (LICENSE.md installed).
- Exact approved archive:
  `python-pywal16-1:3.8.15-1-any.pkg.tar.zst`, SHA-256
  `702b2659076b0ca0f55030d2f215837e2b43064043b5d00fa52b4f497aede1ed`.
  This approval covers no other version, architecture, or build.
