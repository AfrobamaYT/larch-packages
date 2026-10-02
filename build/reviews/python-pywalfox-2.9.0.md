# python-pywalfox 2.9.0-1, any

- Provenance: the PyPI sdist `pywalfox-2.9.0.tar.gz`, whose sha256 the recipe
  pins; its `pywalfox/` package is identical to Frewacom/pywalfox-native tag
  `v2.9.0` on commit `2622afac5995` (2026-05-02, unsigned). The sdist differs
  from the tag only in packaging files (PKG-INFO, egg-info, setup.cfg; the
  tag's .github and scripts/ are not in it).
- The local PKGBUILD is the AUR recipe at `af862b7` (2026-06-22), unchanged.
- Capabilities (1,495 lines of Python):
  - A Firefox native messaging host. Its manifest
    (`/usr/lib/mozilla/native-messaging-hosts/pywalfox.json`) admits only the
    extension `pywalfox@frewacom.org`, which a person installs from Mozilla's
    add-on site; without it nothing starts the host.
  - On the extension's request it reads pywal's colours from `~/.cache/wal`,
    writes `userChrome.css`/`userContent.css` into the default Firefox
    profile's chrome directory, and answers `pywalfox update` over a Unix
    datagram socket `$TMPDIR/pywalfox_socket_<uid>`. `pywalfox log` opens its
    log in `$EDITOR`.
  - No network, no privilege.
- Needed by: hydradevx, merahypr.
- Dependencies: python (Arch's repositories). The manifest names
  `/usr/lib/python3.14/site-packages/...`: the next Python version needs a
  rebuild, as every Python package does.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- Release VM, 2026-09-30, installed from the image of that day with [larch]
  (fix proof p24): the wave's six archives installed with `pacman -U`;
  hydradevx (merahypr still waits for hypr-dock), which had stopped at this
  package, fetched complete and switched there and back, as did the rest of
  the wave's eight rices.
- License: MPL-2.0.
- Not done: the message handling and the file writes were read, the rest
  covered by greps.
- Exact approved archive:
  `python-pywalfox-2.9.0-1-any.pkg.tar.zst`, SHA-256
  `ebadc62853e7bc53cb4e01e581f22c4ebacefafc60c8b3140a683f571e381507`.
  This approval covers no other version, architecture, or build.
