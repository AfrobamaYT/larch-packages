# hyprland-preview-share-picker-git 0.2.1.r16.g0ef9b30-1, x86_64

- Upstream source is the fixed commit
  `0ef9b302aee716f36ea19e33ff3cc457d8c075a8` (merge of pull request #26,
  2026-08-24; `git describe`: `v0.2.1-16-g0ef9b30`). Its submodule
  `lib/hyprland-protocols` is pinned by the tree to
  `3a5c2bda1c1a4e55cc1330c782547695a93f05b2`. The project is MIT licensed.
- Local PKGBUILD at `78575c286f6cadc1efaa1ef633ce839d43033160` is the AUR
  recipe at `1aa950b` (2026-06-20) with three changes: the git source is
  pinned to that commit instead of the branch head, `pkgver` names what
  `pkgver()` computes for it, and the MIT notice is installed, since [larch]
  redistributes the binary. `cargo fetch --locked` and `cargo build --frozen`
  resolve from the commit's `Cargo.lock`, which has no git dependencies.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `pkgbuild2`. All 40 crate versions the binary names are the
  ones in `Cargo.lock`. The package holds the binary, its `schema.json` and
  the license, byte-identical to upstream's; no setuid or group-writable file.
- The program runs as the person, started by xdg-desktop-portal-hyprland
  when `xdph.conf` names it as `custom_picker_binary`. It opens no network
  connection; it asks Hyprland for windows and monitors over Hyprland's local
  IPC socket and captures previews over Wayland. It runs one external
  command: the region selector from the person's own configuration (default
  `slurp -f '%o@%X,%Y,%W,%H'`), split with shlex and executed without a
  shell; its output must match a fixed pattern.
  `build.rs` runs `git describe` and `git log` at build time only.
- Finding, low: the default log file is the fixed path
  `/tmp/hyprland-preview-share-picker.log`, created with `File::create`,
  which follows a symlink placed there by another account. systemd's
  `fs.protected_symlinks = 1` (measured on the owner's machine) refuses to
  follow another user's symlink in the sticky `/tmp`, and Larch has one
  person per machine; `--logs` moves the file.
- Not in use yet: since the security review (`89fc187`) `config/hypr/xdph.conf`
  names no custom picker and XDPH's own picker is what screen sharing shows.
  This approval only lets [larch] carry the package.
- Exact approved archive:
  `hyprland-preview-share-picker-git-0.2.1.r16.g0ef9b30-1-x86_64.pkg.tar.zst`,
  SHA-256 `2653783ea98106bf916f773546c8e28fe1936260203cbbd6188034f13485ca55`.
  This approval covers no other version, architecture, or build.
