# agsv1 1.9.0-3.1, x86_64

- What it is: Aylur's GTK Shell v1.9.0, the final v1 release, installed as
  `/usr/bin/agsv1` beside modern AGS for rices written for v1 (aworldc).
  Internally it still calls itself ags: `~/.config/ags/config.js`, session
  bus name `com.github.Aylur.ags.ags`, cache `~/.cache/ags`, PAM service
  `ags`. None of its files overlap with AGS 3, which owns `/usr/bin/ags`.
- Provenance:
  - Tag `v1.9.0` ("Final version of v1", 2024-11-14) points at
    `67b0e31ded361934d78bddcfc01f8c3fcf781aad` on branch `v1`; neither tag
    nor commit is signed. The recipe's sha256 equals the download, and its
    content equals `git archive v1.9.0`.
  - libgnome-volume-control (bundled as libgvc) is pinned to
    `0a4eda0cdc2deb352bebc70ec697c42af46094e4` with the checksum of its
    `git archive`, from GNOME's GitHub mirror, which yields the same checksum
    as gitlab.gnome.org. AGS v1.9.0's own submodule pin is `8e7a5a4c`, an
    ancestor 48 commits back; public headers, `meson.build` and
    `meson_options.txt` are identical between the two.
- The recipe: kotontrion/PKGBUILDS at `580117dd`, directory `agsv1/` (0BSD),
  the maintainer's own. agsv1 was never published in the AUR (the
  maintainer's AUR comment 998455 on aylurs-gtk-shell; `agsv1/.noaur`).
  Every commit touching `agsv1/` carries a good signature from a key GitHub
  serves for kotontrion, except 1.9.0-3, a squash merge of a third-party pull
  request whose head commit kotontrion signed with identical content. Larch's
  changes:
  - the libgvc pin above, instead of the moving default branch with `SKIP`;
  - `npm ci --ignore-scripts --no-audit` in prepare() against the tarball's
    `package-lock.json`, instead of `npm install` in build(), which neither
    enforced the lock nor stayed off the network for audits;
  - the lockfile's TypeScript 5.3.3 first on `PATH`: Arch's typescript 6
    deprecates `moduleResolution=node10` and `baseUrl`, both in
    `tsconfig.json`;
  - `-Dbuild_types=false`: the 61.6 MB editor type tree is not shipped;
    nothing reads it at runtime;
  - license GPL-3.0-or-later (upstream) and GPL-2.0-or-later (libgvc).
- The lockfile has 166 entries, each with a registry.npmjs.org URL and a
  sha512; all 162 distinct tarballs were downloaded and match. None has an
  install script or `binding.gyp`, and npm ran with `--ignore-scripts`. The
  build uses TypeScript and the `@girs` type packages; the 133 eslint entries
  are installed but never run. The 9 advisories OSV lists for the locked
  versions are all in that unused eslint part. What executes at build time:
  node running `tsc`, g-ir-scanner and meson's `post_install.sh`.
- Capabilities of AGS v1:
  - It runs the person's config with full user rights and gives it command
    execution (`GLib.shell_parse_argv` and `Gio.Subprocess`, no shell), HTTP
    through libsoup3, file reads and writes, and PAM password checks under
    service `ags` (`/etc/pam.d/ags` includes `login`; no setuid).
  - By design it exports `RunJs`, `RunFile` and `RunPromise` on the session
    bus (`src/dbus/com.github.Aylur.ags.xml`): any process on the person's
    session bus can run JavaScript inside AGS, as it could run programs as
    the person anyway.
  - With the matching services loaded it is the notification daemon (every
    notification is kept as plain JSON and PNG in
    `~/.cache/ags/notifications`), the tray host, and downloads cover art
    from any URL a media player advertises.
  - AGS v1 has no session-lock protocol: a lock screen built with it is an
    overlay window, and if AGS crashes the session is unlocked.
  - No hard-coded servers or telemetry, no setuid, polkit or sudo code.
- aworldc: its `~/start.sh` and `~/power.sh` call `ags -r`; this package has
  no `/usr/bin/ags`, so those two key paths need the rice's curated fix to
  name `agsv1` (Larch's post-install for aworldc rewrites only its
  `exec-once` lines).
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; the archive's `.BUILDINFO` records the sha256
  of this PKGBUILD. The file list: `/usr/bin/agsv1` (a link to the launcher),
  `/etc/pam.d/ags` (a backup file), `libgvc.so`, `libgutils.so` and their
  typelibs under `/usr/lib/ags`, the launcher, gresource bundle and two
  `.gir` files under `/usr/share/com.github.Aylur.ags`. The libraries link
  only glib, libpulse and pam. No file is setuid or group-writable.
- Release VM, 2026-09-30: installed with `pacman -U` beside the other eight
  packages of this set and caelestia's six; `agsv1 --version` printed 1.9.0,
  and a one-window config drew its layer on Arch's gjs.
- License: GPL-3.0-or-later and GPL-2.0-or-later (the GPL texts come from
  Arch's licenses package).
- Not done: the widget code of AGS (core, utils and services were read);
  libgvc's C code beyond greps and a summary of its 48-commit change;
  TypeScript 5.3.3's own code; npm registry signatures.
- Exact approved archive:
  `agsv1-1.9.0-3.1-x86_64.pkg.tar.zst`, SHA-256
  `9f1be1ae6a940ece7b8d50109633691bee8f7e9cc29382a40dace53c4eac0549`.
  This approval covers no other version, architecture, or build.
