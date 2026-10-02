# waypaper 2.9-1, any

- Provenance:
  - Upstream tag `2.9` is an annotated, unsigned tag (`4b1c1685`) on the
    unsigned commit `7c1f0b3db4e666533822c2682b7ad42373ff18e8`.
  - The recipe's sha512 equals the download (sha256
    `372c40c82546ec7d57efc0346552d307a5b548de2bac21547da8b148385bfad7`), and
    the unpacked tarball is identical to `git archive` of the tag.
- The local PKGBUILD is the AUR recipe at `3dcfc55` (2026-09-12), unchanged.
  It builds a wheel with `python -m build --no-isolation` and installs it;
  nothing is downloaded. The build runs upstream's `setup.py`, which only
  reads the version and README.
- Dependencies: two are not in Arch's repositories and are reviewed and
  approved beside it: `python-screeninfo` (imported unconditionally) and
  `python-imageio-ffmpeg` (video thumbnails).
- Capabilities:
  - Shell injection through file names: `changer.py:350` runs
    `echo 'loadfile "{image_path}"' | socat - /tmp/mpv-socket-{monitor}` with
    `shell=True`. A wallpaper whose file name contains `'` runs commands as
    the person. It fires only with the mpvpaper backend, while mpvpaper runs
    on that monitor and socat is installed, on a pick, `--random` or the
    slideshow daemon. Rices bring wallpaper folders from third parties. Of
    the seven catalogue rices whose fetch named waypaper (anantnrg,
    kaonkaon-hyprland, maximrichter, namiconfig, one-white-pro, pahasara,
    sunwoo101), none sets `backend = mpvpaper` (three set swww, awww or
    hyprpaper, four ship no waypaper config), and no file in their checkouts
    has a `'` in its name (checked 2026-09-30).
  - Monitor names are interpolated into shell commands too (`app.py:955`,
    `app.py:1109`). `post_command` from the config runs through a shell by
    design, with its substituted values quoted.
  - It starts swww-daemon, awww-daemon or hyprpaper when they are not running,
    even while only building its `--monitor` choices, and kills backends with
    `killall`, `kill -9` on `pgrep -f` matches, `pkill -f waypaperd` and
    `pkill -x hyprpaper`.
  - The mpv IPC socket sits at a predictable path in `/tmp`.
  - No network, no privilege, no telemetry. It writes
    `~/.config/waypaper/config.ini`, `~/.local/state/waypaper/state.ini` and
    `~/.cache/waypaper`, which "clear cache" deletes.
  - It ships a systemd user unit for its slideshow daemon
    (`/usr/share/systemd/user/waypaperd.service`), not enabled. Its GUI can
    start the daemon detached, and `--restore` restarts it.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`, with the two dependencies above installed from
  their approved archives; the archive's `.BUILDINFO` records the sha256 of
  this PKGBUILD. The file list matches the recipe: `/usr/bin/waypaper`,
  `/usr/bin/waypaperd`, the Python package, desktop file, icon, man page, the
  user unit and the license. No file is setuid or group-writable.
- Release VM, 2026-09-30: installed with `pacman -U` beside the other eight
  packages of this set and caelestia's six; `waypaper --version` printed 2.9.
- License: GPL-3.0-only; LICENSE is the verbatim GPLv3 text without an "or
  later" notice.
- Not done: `app.py` was covered by greps for command, file and network calls
  plus the handlers that use them, not read line by line. Bug seen:
  `Popen(["swww kill"])` (`changer.py:256,261`) names a program that does
  not exist.
- Exact approved archive:
  `waypaper-2.9-1-any.pkg.tar.zst`, SHA-256
  `055304bf6f1045a82c2fe5e268c29573185b2e41ee61969c91c51d0d83e7a433`.
  This approval covers no other version, architecture, or build.
