# aylurs-gtk-shell 3.1.2-1, x86_64

- Provenance: Aylur/ags tag `v3.1.2` on commit
  `bbee2f18939f1ec7ff720e717cf305e73635628f` (2026-04-09, unsigned, a
  lightweight tag), the newest release. The recipe's sha256 equals the
  download
  (`7c9bf38cddfa9661ca3bc70268df0f3124174dad0d6ff85433445816471690f4`), and
  the unpacked tarball is identical to `git archive` of the tag.
- The local PKGBUILD is the AUR recipe at `3d9e58d` (2026-04-09) with one
  change: `npm install` became `npm ci --omit=dev --ignore-scripts`. The
  package ships one npm module, gnim 1.9.1, which package-lock.json pins
  (sha512 integrity checked); the 106 development packages `npm install` also
  fetched are neither built nor shipped, and no npm install script runs. The
  Go modules come from go.sum (esbuild 0.25.10, godbus 5.1.0, cobra 1.10.1,
  json5 1.0.0), built `-mod=readonly`.
- Capabilities (1,217 lines of Go in the `ags` command, 1,616 lines of
  TypeScript in its JS library, gnim 4,377 lines):
  - `ags run` bundles a project with the built-in esbuild (and `sass` or
    `blueprint-compiler` for those files) and starts it with gjs; `ags bundle`
    writes such a bundle as a script. The bundle script writes its JavaScript
    to `${XDG_RUNTIME_DIR:-/tmp}/<name>-ags.js` before gjs loads it; a Larch
    session always sets XDG_RUNTIME_DIR, so it stays in the person's 0700
    runtime directory.
  - `ags request`, `toggle`, `quit`, `list` and `inspect` talk to running
    instances over the libastal-io socket and D-Bus.
  - `ags init` and `ags types` run `npx -y @ts-for-gir/cli` (unpinned,
    downloaded from npm at that moment) to generate type definitions. None of
    the approved rices calls either (their configs and scripts at the reviewed
    commits, 2026-09-30); they are developer commands a person types.
  - No privilege: no setuid file, no service, unit or rule in the archive.
- Needed by: cyberarch and gitkhym (their shells) and HyprPanel (its runtime).
- Dependencies: gjs, gtk4-layer-shell, gobject-introspection and npm from
  Arch's repositories; libastal and libastal-4 from this wave.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; its `.BUILDINFO` records the sha256 of this
  PKGBUILD. No file is setuid, setgid or group- or world-writable, and the
  archive holds no D-Bus service, systemd unit, autostart entry, udev or
  polkit rule.
- Release VM, 2026-09-30 (fix proofs p16, p17 and p19): the wave's archives
  installed together with `pacman -U`; all eight rices that had stopped at
  these packages -- hyprland-unrounded, roccorakete-arch-dotfiles, n6v26r,
  shenghuipang, simboi, rudra, cyberarch and gitkhym -- fetched complete and
  switched there and back with their shells drawing (n6v26r and simboi after
  fixes of their own, dd4462bc and 6f989cc4).
- License: GPL-3.0-only.
- Not done: the Go command and the JS library were read around every process
  start, file write and socket; gnim was compared against its registry
  integrity, not read line by line.
- Exact approved archive:
  `aylurs-gtk-shell-3.1.2-1-x86_64.pkg.tar.zst`, SHA-256
  `2d433a757ac9dca0b9cfb964a639e6a24123c5514f2300de732671c1f251d963`.
  This approval covers no other version, architecture, or build.
