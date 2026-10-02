# workstyle-git 0.9.0.r146.gdae1501-1, x86_64

- Provenance: pierrechevalier83/workstyle
  `dae15018c84c4f0feaf498d3676271ca0e3bec44` (2025-10-19), the last commit.
- The local PKGBUILD is the AUR recipe at `adfe61b` (2020-02-23), which built
  whatever the default branch held, pinned to that commit; cargo builds
  `--locked`; `license` names MIT, which Cargo.toml declares -- the repository
  ships no licence text, so the recipe's own `LICENSE` carries the MIT text
  with the copyright line of Cargo.toml's authors (Pierre Chevalier) and says
  where both come from; it is installed to /usr/share/licenses/workstyle-git.
- Capabilities (732 lines of Rust): renames workspaces over the compositor's
  IPC (i3/sway protocol, Hyprland) after the programs in them; writes a
  default `~/.config/workstyle/config.yml` when there is none. No network.
- Needed by: kyoshiro.
- Dependencies: none at run time.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- License: MIT (declared in Cargo.toml).
- Not done: greps for processes, files and network plus the code around every
  hit, not a line-by-line reading.
- Release VM, 2026-09-30, image of that day with [larch] (base 033fc7cc, proof
  run p25 on release VM 2): installed with `pacman -U`; kyoshiro fetched
  complete and switched there and back.
- Exact approved archive:
  `workstyle-git-0.9.0.r146.gdae1501-1-x86_64.pkg.tar.zst`, SHA-256
  `d71bb8cc95a67cce010deb74b6d86f2d13d7a8e7f1c5b3cdeb8a54be1268a554`.
  This approval covers no other version, architecture, or build.
