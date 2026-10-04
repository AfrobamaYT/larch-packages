# python-sherpa-onnx 1.13.8-1, x86_64

For the assistant's English voice (Kokoro, cmd/larch-assistant).

- Provenance:
  - Upstream tag `v1.13.8` of k2-fsa/sherpa-onnx is a lightweight tag on
    `11afbd009a7f8c08f4bcf2fc1b265d0df4670fbf` ("Release v1.13.8 (#3945)", a
    merge made in GitHub's web interface and signed by GitHub, 2026-09-10).
  - The recipe's sha256 for the tag tarball equals the download, and the
    unpacked tarball equals `git archive 11afbd00` (symlinks compared as links).
  - Eleven dependency archives come with it. Each one's sha256 equals the hash
    the project that uses it pins in its own cmake file:
    - sherpa-onnx itself pins eigen 5.0.1, its espeak-ng fork at `ed530aa1`,
      hclust-cpp 2026-02-25, nlohmann/json 3.12.0, kaldi-decoder 0.3.0,
      kaldi-native-fbank 1.22.3, openfst 1.8.5-2026-07-09, its piper-phonemize
      fork at `f3ff95af`, and simple-sentencepiece 0.7.
    - kaldi-native-fbank 1.22.3 pins kissfft at `febd4cae`.
    - kaldi-decoder 0.3.0 pins kaldifst 1.8.0.
- The local PKGBUILD is the AUR recipe `sherpa-onnx` at `2fbfea7` (2026-09-10)
  with these changes:
  - Only the Python bindings; the AUR split also built the C library and its
    commands.
  - Built without portaudio, the websocket server and client, the C API and
    the commands. That drops four archives, among them portaudio from
    hf-mirror.com, and the cargs build dependency.
  - No `sherpa-onnx-cli`: it needs click, and the assistant imports the
    module, not the command.
  - `depends` without `python-onnxruntime` and `alsa-lib`. The module links
    Arch's `libonnxruntime.so` directly, and its ALSA class is the stand-in
    sherpa-onnx builds without ALSA.
  - sentencepiece and pypinyin are `optdepends`. `utils.text2token` imports
    them when called, for keyword and hotword tokens.
  - build() runs behind a proxy that does not exist (`127.0.0.1:9`). The log
    shows every dependency taken from the local archives ("Found local
    downloaded …"), and onnxruntime from `/usr/lib/libonnxruntime.so` and
    `/usr/include/onnxruntime`.
  - `license` names what is compiled in. The AUR said Apache-2.0 only, though
    espeak-ng (GPL-3.0-or-later) is linked in.
- Capabilities:
  - With the websocket parts off, the compiled C++ (`sherpa-onnx/csrc`,
    `python/csrc`) has no network, process or socket code. The one hit is
    `system("clear")` in a terminal display helper for the commands.
  - The Python package has no network or subprocess code. It reads the model
    files it is given and writes a WAV file when asked (`write_wave`).
  - No privilege, no persistence, no telemetry.
- Built with `makechrootpkg -c` in a clean chroot in the disposable
  development VM `voices` (`MAKEFLAGS=-j2`, 6 minutes); the archive's
  `.BUILDINFO` records the sha256 of this PKGBUILD.
  - 32 files, 2.4 MiB packed, 6.7 MiB installed. One shared object (the
    extension, everything else linked into it) and no command.
  - Nothing is setuid or group-writable.
  - makepkg also wrote `python-sherpa-onnx-debug`; [larch] publishes no
    debug packages.
- Voice VM, 2026-10-04: installed with `pacman -U` beside piper-tts.
  - `import sherpa_onnx` reports 1.13.8 on onnxruntime 1.29.0.
  - The assistant's own Kokoro code (`kokoro-en-v0_19`, sha256 as the engine
    pins it, speaker 0) said a 21-word answer in 6.8 s, made in 2.4 s.
  - Parakeet (`parakeet-cli`, as the engine hears) recognised it word for
    word: word errors 0.00.
- License: Apache-2.0 (sherpa-onnx, kaldi-decoder, kaldi-native-fbank,
  kaldifst, openfst, simple-sentencepiece), GPL-3.0-or-later (espeak-ng), MIT
  (nlohmann/json, piper-phonemize), BSD-2-Clause (hclust-cpp), BSD-3-Clause
  (kissfft), MPL-2.0 (Eigen). Their notices are not shipped.
- Not done:
  - The bundled C++ beyond greps for network, process and socket calls.
  - Which of sherpa-onnx's model families besides Kokoro work. Only Kokoro
    was run.
