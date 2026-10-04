# swaylock-effects 1.7.0.0-4, x86_64

- Provenance: upstream tag `v1.7.0.0` on commit
  `4f2234c6bca3ce80dce1dbf7407825a38d58103c` (2023-12-02, unsigned) of
  jirutka/swaylock-effects. One commit followed (2023-12-30); the repository
  has been quiet since March 2024. The recipe's sha256 equals the download
  (`e94d79e189602694bedfbafb553ce3c6c976426e16f76d93bf7e226dc2876eb6`), and
  the unpacked tarball is identical to `git archive` of the tag.
- The local PKGBUILD is the AUR recipe at `c614e0b` (2026-03-16), unchanged:
  meson and ninja; nothing is downloaded during the build. In March its
  maintainer switched the source to another fork (hboetes, 1.8.1) and back
  six days later; `c614e0b` is the recipe from before the switch.
- Code: the fork last merged swaylock at `b4e3a2b` (2023-01-27, 1.7 plus
  eight commits). `pam.c`, `comm.c` and `shadow.c` are byte-identical to
  swaylock 1.7.2; `password.c` differs only in the grace period. Swaylock has
  since changed its authentication path ten times up to 1.8.6 ("Stop
  processing auth requests after success", "Better handle subprocess
  crashes", "Only submit password if previous validation completed", ...);
  none is marked a security fix, and this package has none of them. Where
  the password subprocess dies, swaylock 1.7 exits and leaves the session
  locked; larch-lock's takeover catches that (cmd/larch-lock).
- What it installs: `/usr/bin/swaylock`, `/etc/pam.d/swaylock`, the man page
  and bash, fish and zsh completions. It provides and conflicts with
  swaylock; pacman does not replace swaylock with it unasked (`pacman -U
  --noconfirm` refused in the release VM), which is why cmd/larch-rice gives
  every swaylock rice this package once [larch] serves it.
- Capabilities:
  - Locks through ext-session-lock-v1 and checks the password with PAM
    (`/etc/pam.d/swaylock`) in a forked subprocess, as swaylock does. Built
    with PAM, so not setuid.
  - `screenshots` captures the outputs (wlr-screencopy) and draws them, with
    the rice's effects, behind the lock -- in memory only. How readable the
    desktop stays behind it is the rice's blur.
  - The grace period (`grace`) unlocks on any key, mouse or touch without a
    password while it runs, counted on a clock that stands still in sleep.
    larch-lock passes `--grace 0`, parsed after the config, which turns it
    off.
  - `effect-custom` compiles a C file with `cc` through `system()` or loads a
    shared object into the locker: the rice's own code, trusted as its
    scripts are. None of the 190 fetched rices uses it.
  - No network, no service. It runs when larch-lock starts it.
- Dependencies: libxkbcommon, cairo, gdk-pixbuf2, pam, and OpenMP from
  gcc-libs -- all in Arch's repositories.
- Built with `makechrootpkg -c` in a clean chroot in the release VM
  `larch-release`, 2026-10-03; the source passed its sha256 check before the
  chroot build, and `.BUILDINFO` records the sha256 of this PKGBUILD
  (`e4f7b60a51997e5a94d88f53677ef67ca7fd3b21295816b26cc8261c964813f9`). The
  archive holds the files above; no file is setuid or group-writable.
- Release VM, 2026-10-03: installed over swaylock 1.8.6 (the conflict
  answered by hand). dofiles -- effect-blur, clock, screenshots and
  daemonize in its config -- locked on SUPER+L through larch-lock with its
  blurred screenshot and clock, as `swaylock -C <its config without
  daemonize> --grace 0`; the password unlocked.
- License: MIT.
- Exact approved archive:
  `swaylock-effects-1.7.0.0-4-x86_64.pkg.tar.zst`, SHA-256
  `a9877f55d22266cbbe8da7b97b8c7a3331ca50cb694558736cb44aef7d319051`.
  This approval covers no other version, architecture, or build.
