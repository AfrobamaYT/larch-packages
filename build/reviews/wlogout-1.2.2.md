# wlogout 1.2.2-0, x86_64

- Upstream tag `1.2.2` is a lightweight tag on
  `2db390f3bb1f57e73b3172a7c24f4c1fe35c0c96`. That commit is signed by the
  key the recipe names.
- The release tarball is 542,612 bytes, SHA-256
  `70742b32479ae34ed544ce1fe5b6d92845857d4c4dfe55fccd4eb993f0dd0d9e`. Its md5
  `2d129a847cdf9aa212b834f690f86e4a` is the recipe's pin.
- The tarball's detached signature verifies with
  `F4FDB18A9937358364B276E9E25D679AF73C6D2F` (Haden Collins, RSA-4096, made
  2024-04-22). That is the recipe's only `validpgpkeys` entry. GitHub,
  keyserver.ubuntu.com and keys.openpgp.org serve the same key, and makepkg
  checked the signature again in the build.
- The tarball's 29 files equal `git archive 1.2.2`.
- The local PKGBUILD at `318a0024da34de008aa43ffe045ddeb6b6d77000` is the AUR
  recipe at `9904ef2`, unchanged.
- wlogout runs one command: the action of the button that is clicked, or of
  its key. It runs through `system()` (`/bin/sh -c`, `main.c:763`) after its
  window closes; Esc runs nothing.
  - The actions come from the first layout found: `-l`,
    `$XDG_CONFIG_HOME/wlogout/layout`, `/etc/wlogout/layout`,
    `/usr/local/etc/wlogout/layout`.
  - The packaged `/etc/wlogout/layout` runs `loginctl lock-session`,
    `systemctl hibernate`, `loginctl terminate-user $USER`,
    `systemctl poweroff`, `systemctl suspend` and `systemctl reboot`.
  - It has no other process execution, no network code and no privilege use,
    and it writes no file.
- The layout parser trusts its file. More than 100 buttons overflow a fixed
  array (`main.c:383-389`, `702`), and a key before the first object writes
  `buttons[-1]`. That file can already run any command, so this crosses no
  trust boundary.
- Build: meson generates `config.h` and the two man pages (scdoc) and
  downloads nothing.
- Built with `makechrootpkg -c` in a clean chroot in the disposable development
  VM `rice-pkgs`. `.PKGINFO` and the file list match the recipe:
  - `/usr/bin/wlogout`;
  - `/etc/wlogout/layout` and `style.css`;
  - icons under `/usr/share/wlogout`;
  - man pages, shell completions and the license.

  No file is setuid or group-writable.
- Recipe details, kept as the AUR has them:
  - `pkgrel=0`;
  - plain `meson setup`, which makes a debug build;
  - `/etc/wlogout/*` is not in `backup=()`, so edits there are replaced on
    upgrade. The rices that use wlogout bring their own layout in their
    config.
- License: MIT. The icons are "Creative Commons 3.0" according to
  `assets/CREDIT.md`.
- Exact approved archive:
  `wlogout-1.2.2-0-x86_64.pkg.tar.zst`, SHA-256
  `0c25d965e8825cbf96b084814c774d2643ac35bae9606456b10c6bf31be86990`.
  This approval covers no other version, architecture, or build.
