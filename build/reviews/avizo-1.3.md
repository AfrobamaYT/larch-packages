# avizo 1.3-1, x86_64

- Provenance: upstream tag `1.3` on commit
  `79367b2e363f4fb6235819d8e574d72d6e2f79e4` (2024-01-27, unsigned), the
  newest release. The recipe's sha256 equals the download
  (`2b1f5817a916e518b0c10c4c94a3678a5054b879eb32c10b5d1425faa6387127`), and
  the unpacked tarball is identical to `git archive` of the tag.
- The local PKGBUILD is the AUR recipe at `16e8df6` (2025-03-22), unchanged:
  meson and ninja with Vala; nothing is downloaded during the build.
- What it installs: `avizo-service` and `avizo-client` (Vala, 747 lines in
  total), the helper scripts `volumectl` and `lightctl`, and
  `/etc/xdg/avizo/config.ini`.
- Capabilities:
  - `avizo-service` owns `org.danb.avizo.service` on the session bus and
    draws the volume or brightness bubble on a layer-shell surface; the
    client sets its properties and calls `show`. Configuration is read from
    the XDG config directories, images from `~/.local/share/avizo`.
  - `volumectl` and `lightctl` change volume (pamixer, pactl) and brightness
    (brightnessctl or light) by numbers they check with `expr` before use;
    no `eval`, no shell built from input.
  - No network, no privilege, no process started by the service.
- Dependencies: alsa-utils, cairo, dbus, glib2, glibc,
  gobject-introspection, gtk-layer-shell, gtk3, pamixer -- all in Arch's
  repositories.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD, and the archive holds `avizo-service`, `avizo-client`,
  `volumectl`, `lightctl` and `/etc/xdg/avizo/config.ini`. No file is setuid
  or group-writable.
- Release VM, 2026-09-30 (fix proof p10): installed with `pacman -U`; the rice
  a, which had stopped at avizo, fetched complete and switched there and back.
- License: GPL-3.0-only.
- Exact approved archive:
  `avizo-1.3-1-x86_64.pkg.tar.zst`, SHA-256
  `2df9bccbf439c745733f0d8c9380c2e217ef3867db8e9b4005a8bdb9cdba4200`.
  This approval covers no other version, architecture, or build.
