# clipse 1.2.1-1, x86_64

- Provenance:
  - Upstream tag `v1.2.1` is a lightweight tag on
    `95d666b6cd8cbaec22732d605bc838365f144617`, a merge made in GitHub's web
    interface and signed by GitHub (2026-01-27).
  - The recipe's sha256 for the tag tarball equals the download, and the
    unpacked tarball is byte-identical to `git archive 95d666b6`.
- The local PKGBUILD is the AUR recipe at `7760fcb` (2026-03-30, pushed by
  upstream's own CI) with these changes:
  - `go mod tidy` is gone. It rewrote go.mod/go.sum and downloaded all 51
    modules during build(), unpinned.
  - prepare() runs `go mod download`, which checks every module against
    go.sum. build() runs with `GOPROXY=off`, `GOTOOLCHAIN=local` and
    `-mod=readonly`, so a module go.sum does not pin fails the build.
  - `arch=('x86_64')`, since it ships a native binary, and
    `license=('MIT')`, upstream's license, which is now installed. The AUR
    said `any` and GPL.
- go.sum has 130 lines. Every module was downloaded from proxy.golang.org,
  its hash recomputed and compared with go.sum and sum.golang.org: 130 of 130
  match. There are no `replace` lines and no `vendor/`. The build compiles
  42 packages from 24 modules, all pinned. Built with Arch's Go 1.27.1 and no
  toolchain download.
- Capabilities:
  - No network code in the compiled packages.
  - It runs `pgrep`/`ps` through `sh -c` without user input, `pkill -f` on
    its own name for `-kill` (which also hits unrelated processes whose
    command line contains "clipse"), `kill`, and `wl-copy`/`wl-paste` as
    argument lists. Two detached `wl-paste --watch` watchers outlive the
    terminal.
  - Its `sh -c` redirections use a path from the person's own config.json
    plus a timestamp; clipboard content never reaches a shell.
  - Bug: `shell/common.go:164-166` tests `strings.Contains("wl-paste", exe)`
    with the arguments reversed. `-listen` and `-pause` therefore send
    SIGTERM to every one of the person's processes whose name is a substring
    of "wl-paste": other clipboard watchers such as cliphist's `wl-paste`,
    the `st` terminal, `paste`. A rice that starts `clipse -listen` stops
    them.
  - It keeps the clipboard history in plaintext under `~/.config/clipse`
    (files 0644, the log 0666 before umask) and respects
    `CLIPBOARD_STATE=sensitive`.
  - No privilege. Auto-paste (off by default) needs `/dev/uinput`; upstream
    suggests an `input` group udev rule for it. Larch ships none.
  - No persistence, no telemetry.
- Known advisories (OSV): golang.org/x/sys GO-2026-5024 affects only
  `x/sys/windows`, which is not compiled in. None in the other compiled
  modules.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `rice-pkgs`; the archive's `.BUILDINFO` records the sha256
  of this PKGBUILD. `.PKGINFO` and the file list match the recipe:
  `/usr/bin/clipse`, a PIE that loads through the dynamic loader but links
  no shared library, and the license. No file is setuid or group-writable.
- Release VM, 2026-09-30: installed with `pacman -U` beside the other eight
  packages of this set and caelestia's six; `clipse -v` printed v1.2.1.
  `-listen` was not run.
- License: MIT. The notices of the compiled MIT, BSD-3-Clause and ISC
  dependencies are not shipped.
- Not done: dependency code beyond greps for commands, files and network
  calls; `app/*` and `config/theme.go` were covered by those greps, not read
  line by line; sum.golang.org inclusion proofs. Upstream's AUR bumps come
  from its CI with `updpkgsums`, so an AUR checksum is no independent check:
  every later version needs its own review.
- Exact approved archive:
  `clipse-1.2.1-1-x86_64.pkg.tar.zst`, SHA-256
  `1bcb0e9e6a5370f525a6fed148104d8142f58904492b76d4f05bf29165b35066`.
  This approval covers no other version, architecture, or build.
