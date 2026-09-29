# hyprlang2lua 0.7.1-1, x86_64

- Upstream tag `v0.7.1` dereferences to `65921f5d1c97c6ebee474fe203a2df9bb1752db2`.
  The source tarball SHA-256 is
  `fa041a0393e1e1828c42e67058546d8adb27f4c585856752e385f1f1d5cfcc0e`.
  Its command entry point matched that Git commit byte for byte.
- Local PKGBUILD at `9b97aa4aa149432cc3cb0eb37652b0304c8f5258` pins
  the source hash, runs `go test ./...`, and packages the converter, README,
  and MIT license. The built package's `.PKGINFO` and file list matched that
  recipe. Build and test succeeded in the disposable development VM; the
  package installed there.
- The runtime Go files at the pinned commit use no `os/exec`, network package,
  `syscall`, `unsafe`, or dynamic plugin loader. The CLI reads stdin or a
  requested `.conf` tree and writes Lua to stdout, `--out`, or adjacent `.lua`
  files under `--dir`. Larch's importer invokes it on a private Rice copy.
- Exact approved archive:
  `hyprlang2lua-0.7.1-1-x86_64.pkg.tar.zst`, SHA-256
  `e53c81fba26bca489534f3270b30e69a84fd4daab23d7936865ddfca51eac378`.
  This approval covers no other version, architecture, or build.
