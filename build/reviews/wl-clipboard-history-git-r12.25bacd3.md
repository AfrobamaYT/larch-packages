# wl-clipboard-history-git r12.25bacd3-1, x86_64

- Provenance: janza/wl-clipboard-history
  `25bacd3fd752ca02d316beb0bb16b8468da4f6a0` (2019-09-16), the last commit of
  the repository.
- The local PKGBUILD is the AUR recipe at `32a74ad` (2019-03-25), which built
  whatever the default branch held, pinned to that commit; `makedepends` names
  git (the clean chroot stopped at "Cannot find the git package needed to
  handle git sources"), and the MIT text (LICENCE) is installed as its licence
  requires. `pkgver` reads what makepkg wrote into the file during the build.
- Capabilities (60 lines of sh):
  - `wl-clipboard-history -t` runs `wl-paste -w wl-clipboard-history`: every
    clipboard change is stored, up to 1,000 entries, in plain text in
    `~/.clipboard.sqlite` -- anything copied, a password too, stays there
    until it rotates out. That is the tool's purpose.
  - The content's single quotes are doubled, so it stays one SQL string
    literal; sqlite3 reads the lines after the statement's first as SQL text,
    so no line of it becomes a dot-command (measured with sqlite3 3.53.4: a
    copied text with `.shell touch` and `.system touch` lines, and one with
    `'); .shell`, stored one row each and ran nothing). The `-l`/`-p`
    arguments go into SQL unquoted; they come from the rice's own scripts.
  - No network, no privilege.
- Needed by: kofta999, garden-hyprland-dotfiles.
- Dependencies: wl-clipboard, sqlite (Arch's repositories).
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable.
- Release VM, 2026-09-30, installed from the image of that day with [larch]
  (fix proof p24): the wave's six archives installed with `pacman -U`;
  kofta999 and garden-hyprland-dotfiles, which had stopped at this package,
  fetched complete and switched there and back, as did the rest of the wave's
  eight rices.
- License: MIT.
- Not done: nothing -- the script was read whole.
- Exact approved archive:
  `wl-clipboard-history-git-r12.25bacd3-1-x86_64.pkg.tar.zst`, SHA-256
  `207859ae33d388e6eafd60037add0601bbd24411c4bd2cbdda173de1a0f8fb2d`.
  This approval covers no other version, architecture, or build.
