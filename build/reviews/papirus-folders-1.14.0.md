# papirus-folders 1.14.0-1, any

- Provenance:
  - Upstream tag `v1.14.0` is a signed annotated tag on
    `0f838ee5679229e3a3e97e3b333c222c9e9615b4`, and that commit is signed
    with the same key: the recipe's `validpgpkeys`,
    `1BA35B1B2207A266F6E0AD2AF0EC91A29D2E78EC` (Sergei Eremenko).
  - GitHub's copy of the key shows the signing subkey as expired
    (2025-07-03); keyserver.ubuntu.com's copy extends it to 2035. The build
    took the key from keyserver.ubuntu.com, and makepkg verified the commit
    signature (`?signed`).
  - makepkg's checksum of the Git source (sha256 of `git archive`) and of the
    hook file equal the recipe's.
- The local PKGBUILD is the AUR recipe at `03b24dc` (2025-08-02) with one
  change: the source names commit `0f838ee` instead of the tag. Upstream's
  release step re-tags with `git tag -f` (`Makefile:33`), so a tag can move;
  the commit cannot.
- Nothing is built. package() runs `make install` (the script and bash/zsh
  completions) and installs the license and the pacman hook.
- What runs as root:
  - The hook `papirus-folders.hook`: after every install or upgrade of
    `papirus-icon-theme`, pacman runs `/usr/bin/papirus-folders -R` as root.
    `-R` reads theme and colour from the root-owned
    `/var/lib/papirus-folders/keep` and re-points the folder symlinks in
    `/usr/share/icons/Papirus*/…/places` (files of `papirus-icon-theme`, so
    `pacman -Qkk` reports them as changed). Without a keep file it prints
    "Unable to find config file." and exits 0 (`do_restore_color`,
    `_exit`), changing nothing.
  - Under `sudo -E pacman`, a person-writable `XDG_DATA_HOME` or
    `XDG_DATA_DIRS` would steer that root run into a theme folder the person
    controls.
  - The script elevates itself with `sudo` for colour changes
    (`papirus-folders:401-403`).
  - Its `-t` argument accepts any directory with an `index.theme`, the
    current directory first, and theme names are not cleaned (`../`). Run as
    root with a chosen `-t`, it creates symlinks in any directory. The package
    as shipped gives no one that: plain `sudo` asks for the password. Larch
    adds no NOPASSWD sudo or polkit rule for papirus-folders (caelestia-cli's
    `sudo -n papirus-folders` therefore fails, as its review says).
- No network. `eval` is applied only to `declare -p` output, which is
  quoted.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; the archive's `.BUILDINFO` records the sha256
  of this PKGBUILD. The file list matches the recipe:
  `/usr/bin/papirus-folders`, the bash and zsh completions, the hook under
  `/usr/share/libalpm/hooks/` and the license. No file is setuid or
  group-writable.
- Release VM, 2026-09-30: installed with `pacman -U` beside the other eight
  packages of this set and caelestia's six; the hook ran after the install and
  after reinstalling papirus-icon-theme, printed "Unable to find config file.
  Exiting ..." and changed nothing; `papirus-folders -l` listed the colours.
- License: MIT, installed.
- Not done: how `gtk-update-icon-cache` behaves as root on a hostile
  directory; papirus-icon-theme itself.
- Exact approved archive:
  `papirus-folders-1.14.0-1-any.pkg.tar.zst`, SHA-256
  `0f2376178aca2fe3862947d530892612740c220ce42b92521f1970599bde41be`.
  This approval covers no other version, architecture, or build.
