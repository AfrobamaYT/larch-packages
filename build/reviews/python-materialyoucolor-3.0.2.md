# python-materialyoucolor 3.0.2-1, x86_64

- Upstream tag `v3.0.2` is a lightweight tag on
  `25fcd947db53cd8719301d01dbec6e6e707131fa` ("fix build", 2026-02-22,
  unsigned), which is in `main`'s history.
- The source tarball SHA-256 is
  `aa013f0faea26b87b65f35d7b67f7850c7ed4b926cf1628617d088fe9ddaa9ec`. The
  recipe pins it, and a fresh download for this review matched. Its embedded
  commit ID is `25fcd947`, and all 70 files have the Git hashes of that
  commit's tree.
- The vendored `stb_image.h` (v2.29) is byte-identical to nothings/stb at
  `0bc88af`.
- The local PKGBUILD at `318a0024da34de008aa43ffe045ddeb6b6d77000` is the AUR
  recipe at `7a148d4`, unchanged.
- It computes Material You colour schemes; caelestia-cli uses it.
  - It has no network access, no subprocess, no privilege use and no
    telemetry, and on Linux it writes no file.
  - `exec()` in `dynamiccolor/color_spec.py:92-95` runs only over the
    hard-coded names at `:10-79`, to generate method stubs.
  - Android-only code is gated by `ANDROID_ARGUMENT` and never runs here.
- Its C++ extension decodes images with stb (`quantize/celebi.cc:64-87`). Two
  robustness defects:
  - pixels are indexed without a size check (`celebi.cc:47-49`);
  - `quality=0` divides by zero (`:69`).

  caelestia-cli hands it only thumbnails that Pillow has already re-encoded.
- Build: `setup.py` compiles one pybind11 extension from `quantize/*.cc`,
  without network access or subprocesses. `--no-isolation` keeps pip offline.
- Built with `makechrootpkg -c` in a clean chroot in the disposable development
  VM `rice-pkgs`; makepkg's SHA-256 check passed. `.PKGINFO` and the file list
  match the recipe: the `materialyoucolor` package under
  `/usr/lib/python3.14/site-packages` and the license. No file is setuid or
  group-writable.
- License: MIT. The package also bundles ten Apache-2.0 C++ files (Google LLC)
  and stb (MIT or Unlicense).
- Not done: a line-by-line reading of the numeric code (grepped only), and
  the CVE status of stb 2.29.
- Exact approved archive:
  `python-materialyoucolor-3.0.2-1-x86_64.pkg.tar.zst`, SHA-256
  `1ea9d34231fddae35163488d859b33841b5aea09bf79ccc525ded946c9693008`.
  This approval covers no other version, architecture, or build.
