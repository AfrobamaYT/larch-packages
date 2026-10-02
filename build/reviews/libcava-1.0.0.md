# libcava 1.0.0-1, x86_64

- Upstream is `LukashonakV/cava`, a fork of `karlstav/cava` that builds cava's
  core as a library. It is the library caelestia-shell links. Tag `1.0.0` is a
  lightweight tag on `f03278ef9e5e7948fb206453d2f02758f8db216c`, the fork's
  master head. That commit is the merge of its "Upstream sync" (2026-07-20),
  which brought in karlstav/cava up to `4b12c2b` (2026-07-05). The fork reuses
  upstream's version numbers for its own commits.
- The source tarball SHA-256 is
  `437df0a29e52e555357a06238f4c5cbe6d51b5dd4225700cb7adbb19d8bb9474`. The
  recipe pins it, and a fresh download for this review matched. Its content
  equals `git archive f03278ef`.
- The local PKGBUILD at `318a0024da34de008aa43ffe045ddeb6b6d77000` is the AUR
  recipe at `3940344`, unchanged.
- The fork's changes against upstream (`git diff 4b12c2b f03278ef`, 58 files):
  - a meson build that makes the library;
  - public headers under `include/cava/`, plus `libcava.pc`;
  - the main loop moved from `cava.c` into the library;
  - `$VAR` expansion in config paths, done with `getenv` and no shell;
  - `cava_destroy()` now frees the plan itself.

  A grep of the lines the fork adds finds no program execution, socket,
  library loading or privilege use.
- Capabilities:
  - It has no network code. It reaches audio servers only through their
    client libraries.
  - It keeps upstream's terminal-output cleanup, which calls `system()` with
    fixed strings (`setfont`, `setterm`, `clear`).
  - It keeps upstream's config loader, which writes a default config, shaders
    and themes under `~/.config/cava/`.

  caelestia-shell reaches neither of those two. Its Services plugin calls only
  `cava_init`, `cava_execute` and `cava_destroy`
  (`plugin/src/Caelestia/Services/cavaprovider.cpp`). It does not free the plan
  itself, which matches the fork's `cava_destroy`.
- Other defects, noted for anyone else who links the library:
  - `audio_raw_destroy()` frees pointers into its own struct
    (`output/common.c:607-615`).
  - The prototype of `audio_raw_fetch` depends on `SDL_GLSL`, and `libcava.pc`
    does not pass that define on (`include/cava/output/common.h:32-37`).
  - Many library paths call `exit()`.
- Built with `makechrootpkg -c` in a clean chroot in the disposable development
  VM `rice-pkgs`; makepkg's SHA-256 check passed. `.PKGINFO` and the file list
  match the recipe:
  - `libcava.so.1.0.0` and its two links;
  - five headers under `/usr/include/cava`;
  - `libcava.pc`;
  - the MIT license.

  No file is setuid or group-writable.
- License: MIT. The library links fftw, which is GPL-2.0-or-later.
- Not done: a line-by-line audit of cava's upstream code. The fork's changed C
  files were read; the rest of the tree was grepped.
- Exact approved archive:
  `libcava-1.0.0-1-x86_64.pkg.tar.zst`, SHA-256
  `3e92f3c18effbb9cce96a6ee13221fa3325b04f0b85648e6dc7912632e90fc5f`.
  This approval covers no other version, architecture, or build.
