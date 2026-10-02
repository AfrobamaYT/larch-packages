# poweralertd 0.3.0-1, x86_64

- Provenance: ~kennylevinsen/poweralertd on sr.ht, tag `0.3.0` on commit
  `2b54c6486b5d` (2024-04-20, unsigned), the newest release. The recipe's
  sha256 equals the download, and the unpacked tarball is identical to `git
  archive` of the tag.
- The local PKGBUILD is the AUR recipe at `3ede879` (2024-06-03), unchanged.
- Capabilities (1,136 lines of C): reads batteries and power supplies from
  UPower on the system bus and posts desktop notifications on the session bus
  when they change. No processes, files, sockets or network.
  - The package ships a systemd user unit (`poweralertd.service`) that nothing
    enables; the rices start the program themselves.
- Needed by: k0ss4, samir176520.
- Dependencies: glibc, systemd-libs, upower -- all in Arch's repositories.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- Release VM, 2026-09-30, installed from the image of that day with [larch]
  (fix proof p24): the wave's six archives installed with `pacman -U`; k0ss4
  and samir176520, which had stopped at this package, fetched complete and
  switched there and back, as did the rest of the wave's eight rices.
- License: GPL-3.0-only.
- Not done: the 1,136 lines were read around every D-Bus call, not line by
  line.
- Exact approved archive:
  `poweralertd-0.3.0-1-x86_64.pkg.tar.zst`, SHA-256
  `97278e510454328fb61146668726ef992ba2a3fa183d75dae070b55a941273d0`.
  This approval covers no other version, architecture, or build.
