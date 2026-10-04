# piper-tts 1.8.0-1, x86_64

For the assistant's German voice (Piper `de_DE-mls-medium`, cmd/larch-assistant).

- Provenance:
  - Upstream tag `v1.8.0` of OHF-Voice/piper1-gpl is a lightweight tag on
    `639388b6317fc4731e91d53da42aea68fd4166ff` ("Bump version", Michael
    Hansen, 2026-09-04), not signed.
  - The recipe pins the tag's checkout by sha256 (makepkg: "piper1-gpl ...
    Passed").
  - espeak-ng, which upstream's CMakeLists.txt fetched with git while
    building and pinned by the short hash `724808c` only, is a source of its
    own at the full commit `724808c5a83f9ef95fdd0db886ba7ba537ff224a` ("Add
    Abkhazian language support (ab) (#2369)", 2026-04-03, signed by GitHub).
    A commit pin, so no checksum (`SKIP`).
- The local PKGBUILD is the AUR recipe at `e190a7c` (2026-09-05) with these
  changes:
  - espeak-ng from `source=()`: prepare() points the ExternalProject at it
    (`SOURCE_DIR`) and its include path with it, instead of `GIT_REPOSITORY`.
  - build() runs behind a proxy that does not exist (`127.0.0.1:9`), so a
    download the build tries anyway fails. The first build did fail there:
    espeak-ng's own `cmake/deps.cmake` fetches sonic with git when it finds no
    system libsonic, although piper builds it with `USE_LIBSONIC=OFF`.
    `libsonic` (extra) is now a make dependency; the build log says
    `libsonic: OFF (/usr/lib/libsonic.so /usr/include)` and nothing is fetched.
  - No libpiper and no ctest: the Python module does not use the C++ library.
  - No `/usr/bin/piper`: the command imports pathvalidate, which is not in
    Arch; the module, which the assistant imports, does not.
  - `depends` without `onnxruntime` and `pathvalidate`, `optdepends` gone;
    `license` adds Apache-2.0 for g2pW's code, as upstream's setup.py says.
- Capabilities, by grep over `src/piper`:
  - What `import piper` loads (config, voice, phonemizers, g2pW) has one
    network call: `phonemize_chinese.py` downloads the g2pW model from
    huggingface.co the first time a Chinese voice phonemizes, and unpacks the
    tarball with `extractall()` and no filter. Larch uses no Chinese voice.
  - `download_voices.py` (urlopen) and `audio_playback.py` (starts ffplay)
    belong to the command line, which is not shipped; `http_server.py` needs
    Flask, which is not a dependency.
  - espeakbridge.c is the phonemizer binding; espeak-ng is compiled in
    statically with its data (`piper/espeak-ng-data`, 412 files).
  - No privilege, no persistence, no telemetry.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `voices` (`MAKEFLAGS=-j2`); the archive's `.BUILDINFO`
  records the sha256 of this PKGBUILD. 514 files, 33 MiB packed, 45 MiB
  installed; one shared object (`espeakbridge.so`), nothing setuid or
  group-writable. makepkg also wrote `piper-tts-debug`; [larch] publishes no
  debug packages.
- Voice VM, 2026-10-04: installed with `pacman -U`; its dependencies from extra
  came to 437 MiB, most of it `python-onnxruntime-cpu` and what that pulls in
  (scipy, sympy, pillow). The assistant's own synthesis code, run against
  `de_DE-mls-medium` (sha256 as the engine pins it), speaker 96: loaded in
  1.1 s, 6.0 s of speech in 0.7 s while another build ran. A 20-word answer
  came back from Parakeet (`parakeet-cli`, as the engine hears) with one word
  off, "Pakete" for "Paket": word errors 0.05.
- License: GPL-3.0-or-later (piper and espeak-ng), Apache-2.0 (g2pW).
- Not done: espeak-ng's C code beyond the build; the onnxruntime it runs on is
  Arch's.
