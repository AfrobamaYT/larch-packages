# pyprland 3.4.4-1, any

- Provenance: upstream tag `3.4.4` on commit
  `acc4f39b233e6f53d998b69fa01e6359746e3770` (2026-09-03, unsigned), the
  newest release. The recipe's sha256 equals the download
  (`5e9b695ddc4ba7d740168aefcde2f334bd341dd8c2e63c6290941785115e3a1d`), and
  the unpacked tarball is identical to `git archive` of the tag.
- The local PKGBUILD is the AUR recipe at `7ebb36e` (2026-09-03) with one
  change: it deletes `/usr/bin/pypr-gui` and the `pyprland/gui` package
  after installing the wheel (below). `pypr` never imports `pyprland.gui`;
  the rices that need pyprland (avnibilgin, merahypr, degra02,
  maximrichter) call only `pypr` subcommands (checked 2026-09-30).
- Why pypr-gui is left out: its aiohttp server
  (`pyprland/gui/server.py`, `127.0.0.1:18099`, a fixed port) saves and
  applies the pyprland configuration over `POST /api/save` and
  `/api/apply` with no Origin, Host or token check. aiohttp's server-side
  `request.json()` parses any body whatever its content type (3.12.15 and
  3.13.5, `web_request.py:692`), so a web page could send such a request
  as a "simple" cross-site POST without a preflight, or through DNS
  rebinding, while pypr-gui runs. The configuration holds commands:
  `system_notifier` starts the commands of its `sources` as soon as it is
  loaded, so /api/apply is command execution as the person.
- Capabilities of what remains (21,214 lines of Python):
  - The daemon listens on a Unix socket in
    `$XDG_RUNTIME_DIR/hypr/<instance>/.pyprland.sock`; `pypr` and the C
    client `pypr-client` (188 lines, socket path built with `snprintf` and
    a length check) talk to it.
  - Commands from the person's configuration run through a shell by design
    (scratchpads, menus, `system_notifier` sources, wallpaper theme hooks,
    `adapters/fallback.py`).
  - The wallpapers plugin can fetch pictures from Reddit, Unsplash, Picsum
    and Bing when its online mode is configured; nothing else goes to the
    network.
  - No privilege.
- Dependencies: python, python-aiofiles, python-aiohttp, python-pillow --
  all in Arch's repositories.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD, and the archive holds `/usr/bin/pypr`, `pypr-client`,
  `pypr-quickstart`, the Python package without `pyprland/gui`, and the
  license; no `pypr-gui`. No file is setuid or group-writable.
- Release VM, 2026-09-30 (fix proof p10): installed with `pacman -U`; degra02,
  which had stopped at hyprshade and pyprland, fetched complete with its
  Pyprland config linked and switched there and back.
- License: MIT.
- Not done: the 21,214 lines were covered by greps for processes, shells,
  network and files plus the code that uses them, not read line by line.
- Exact approved archive:
  `pyprland-3.4.4-1-any.pkg.tar.zst`, SHA-256
  `8c1af61686c1171dc1088ced745158c09104035b8336e9b5f8073e747a8d9005`.
  This approval covers no other version, architecture, or build.
