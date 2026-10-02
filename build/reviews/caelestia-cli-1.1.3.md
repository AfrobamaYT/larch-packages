# caelestia-cli 1.1.3-1, any

- Provenance:
  - Upstream tag `v1.1.3` is an annotated, unsigned tag on
    `82265df3665b40184e8bdc2165541e072c5a4971`. GitHub's web-flow key
    signed that commit, and it is in `main`'s history.
  - The recipe builds the release asset `caelestia-1.1.3.tar.gz`, uploaded by
    the project's release workflow. Its SHA-256
    `f31447efdd94a18556e338bcf8a38236f34660a56b241657817e6cbe80b067e3` is the
    recipe's pin and GitHub's recorded digest.
- Asset against the tag: all 86 shared files are byte-identical, with the
  same modes.
  - Only in the asset: the generated `PKG-INFO`.
  - Only in the tag: `bin/`, nix files, `.envrc` and `.github/`. These are
    the files `pyproject.toml:20-25` leaves out.
- The local PKGBUILD at `318a0024da34de008aa43ffe045ddeb6b6d77000` and
  `message.install` are the AUR recipe at `a6f5c17`, unchanged.
  `message.install` only prints five lines.
- What it runs: `caelestia` drives caelestia-shell's scheme, wallpaper,
  screenshot, recording and clipboard functions. It does this through local
  programs: `grim`, `slurp`, `swappy`, `wl-copy`, `cliphist`, `fuzzel`,
  `gpu-screen-recorder`, `notify-send`, `sass`, `dconf`, `qs` and Hyprland
  dispatches quoted with `shlex.join`.
  - Its three `shell=True` sites run hook strings; none puts input into the
    command string.
  - Two of those hooks are the user's own `postHook` from `cli.json`.
  - The third runs the hooks of the dotfiles manifest (see the last item).
- Root attempts without asking (`utils/theme.py`). On every scheme or
  wallpaper change it tries:
  - `sudo -n papirus-folders -C <colour> -u` (`:246-251`);
  - for each installed Chromium, Brave or Chrome, `sudo -n mkdir` and
    `sudo -n tee` of `/etc/.../policies/managed/caelestia.json` (`:345-376`).
    The file holds `{"BrowserThemeColor": <surface colour>,
    "BrowserColorScheme": "device"}`.

  caelestia-shell starts such a change on its own at its first start. Larch's
  sudo asks for a password (`%wheel ALL=(ALL:ALL) ALL`, cmd/larch-install), so
  `sudo -n` fails and nothing under `/etc` changes. It succeeds on an install
  made with `--passwordless-sudo`, and in development VMs.
- The upstream README advises two passwordless sudoers rules for this. One
  rule, `tee` into the policy file, would let any process of the user write any
  browser policy as root. Larch does not add them.
- Every scheme change also rewrites whole config files of other programs:
  - `fuzzel.ini`, `htoprc` and `cava/config`;
  - GTK 3 and 4 `gtk.css`;
  - a Discord theme that imports CSS from refact0r.github.io.

  It writes colour escape sequences to every writable `/dev/pts/N`.
- Network access and code from the network:
  - `emoji -f` downloads JSON from raw.githubusercontent.com.
  - `install` and `update` are a dotfiles manager. They clone the unpinned
    `main` of `caelestia-dots/caelestia` and run its manifest's hooks. They
    also build its PKGBUILDs, install and remove packages, and run `-Syu`.

  caelestia-shell calls none of these three. Larch installs the reviewed Rice
  commit itself and never runs `caelestia install`.
- No telemetry, no update check.
- Built with `makechrootpkg -c` in a clean chroot in the disposable development
  VM `rice-pkgs`; makepkg's SHA-256 check passed. `.PKGINFO` and the file list
  match the recipe: `/usr/bin/caelestia`, the `caelestia` package under
  `/usr/lib/python3.14/site-packages` and the fish completion. No file is
  setuid or group-writable.
- License: GPL-3.0.
- Not done: `scheme.py`, `material/generator.py`, `colour*.py` and
  `dots/diff.py` were only grepped. The dotfiles repository that `install`
  would run was not reviewed.
- Exact approved archive:
  `caelestia-cli-1.1.3-1-any.pkg.tar.zst`, SHA-256
  `647bd601cffd735abfd469b8aa7e5fa443b6a5d8e557c777fdc65fec030ec6b3`.
  This approval covers no other version, architecture, or build.
