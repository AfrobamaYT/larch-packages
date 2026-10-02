# grimblast-git r168.57baf31-1, any

- Provenance: `hyprwm/contrib` commit
  `57baf317e5196a8286b80976771ef55febad8660` (2026-08-21, unsigned), the
  last commit touching `grimblast/`. The recipe fetches exactly that commit
  (`#commit=`); `pkgver()` gives `r168.57baf31` there.
- The local PKGBUILD is the AUR recipe at `a0e85f9` (2024-01-07), which built
  whatever the default branch held, pinned to that commit. `licence=` (which
  makepkg ignores) became `license=('MIT')`, and the MIT text from the
  repository root is installed.
- What it installs: `/usr/bin/grimblast` (a 407-line Bash script), its man
  page generated with scdoc, the license.
- Capabilities:
  - Screenshots with grim and slurp, window and output geometry from
    `hyprctl activewindow|workspaces|monitors|clients -j` read with jq, the
    clipboard through `wl-copy`, notifications through
    `notify-send`; an area selection may freeze the screen with
    `hyprpicker -rz`, which it ends with `pkill hyprpicker` (every
    hyprpicker of the person).
  - `hyprctl eval 'hl.layer_rule(...)'` for the selection layer: Lua syntax,
    for Hyprland's Lua config.
  - Files: screenshots to `$XDG_SCREENSHOTS_DIR`, `$XDG_PICTURES_DIR` or
    `$HOME`; `edit` writes to `/tmp` and runs `$GRIMBLAST_EDITOR` (default
    gimp) on it; a lock file in `$XDG_RUNTIME_DIR`.
  - It `source`s `~/.config/user-dirs.dirs` as shell code to find the
    pictures directory. A rice that ships that file is therefore code the
    rice review has to read.
  - `eval "set -- $parsed_args"` evaluates getopt's own quoted output, the
    usual getopt idiom. No network, no privilege.
- Dependencies: hyprland, grim, slurp, jq; optional libnotify, hyprpicker,
  wl-clipboard -- all in Arch's repositories.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD, and the archive holds `/usr/bin/grimblast`, `grimblast.1.gz` and
  the license, nothing else. No file is setuid or group-writable.
- Release VM, 2026-09-30 (fix proof p10): installed with `pacman -U`; lierb,
  which had stopped at grimblast-git and python-pywal16, fetched complete and
  switched there and back.
- License: MIT.
- Exact approved archive:
  `grimblast-git-r168.57baf31-1-any.pkg.tar.zst`, SHA-256
  `4f72de9abe0dec51a845baa26eda59ee4d9417ac9906f221c0463a86a6b250cc`.
  This approval covers no other version, architecture, or build.
