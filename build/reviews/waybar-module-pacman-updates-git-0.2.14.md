# waybar-module-pacman-updates-git 0.2.14-1, x86_64

- Provenance: coffebar/waybar-module-pacman-updates
  `bc772692928bee1a7aa5778af6ab65d34e93abab`, tag 0.2.14.
- The local PKGBUILD is the AUR recipe at `b52f7f1` (2026-07-30), pinned there
  by a short hash, here by the full one; cargo fetches `--locked`.
- Capabilities (828 lines of Rust): a Waybar module counting updates; it runs
  `checkupdates` and `pacman -Qm` and asks the AUR's RPC (aur.archlinux.org)
  for the versions of the foreign packages -- sending their names. No
  privilege.
- Needed by: hyprpunk.
- Dependencies: waybar, pacman, pacman-contrib, curl, openssl.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: GPL-3.0-or-later.
- Not done: greps for processes, files and network plus the code around every
  hit, not a line-by-line reading.
- Release VM, 2026-09-30, image of that day with [larch] (release VM 3 on
  2026-10-01, base 033fc7cc upgraded to that day; after 755dfa25): installed
  with `pacman -U`; hyprpunk fetched complete and switched there and back.
- Exact approved archive:
  `waybar-module-pacman-updates-git-0.2.14-1-x86_64.pkg.tar.zst`, SHA-256
  `3c67b38c0dbb739a0a4a8726b2c592b41bbf4e3a8fb68c4be85a150790bdb768`.
  This approval covers no other version, architecture, or build.
