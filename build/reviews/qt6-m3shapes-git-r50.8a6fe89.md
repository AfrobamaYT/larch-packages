# qt6-m3shapes-git r50.8a6fe89-1, x86_64

- Upstream is `soramanew/m3shapes`, the Material 3 shape library that
  caelestia-shell's QML uses. The pinned commit is
  `8a6fe8961749887d677700b6508e0c9249968b7e` ("namespace everything under
  m3shapes", 2026-09-17), the head of `main`. It was authored and committed
  by the repository's owner `soramanew` and is unsigned, like all 50 commits.
  `git rev-list --count` gives 50, the recipe's `r50`.
- The local PKGBUILD at `d5b5d7b10a0ff4beaa7663f9ae85a220001607c6` is the AUR
  recipe at `f4184f7` with the source pinned to that commit and a comment
  saying why. The AUR recipe builds whatever `main` holds.
- Why r50 and not the AUR's r38.6875533 (measured in the release VM,
  2026-09-29, with the exact archives installed by `pacman -U`):
  - Built at r38, the package put `libm3shapes.so` beside its QML plugin with
    no RPATH to it. caelestia-shell 2.5.0 then failed to load ("Cannot load
    library .../libm3shapesplugin.so: libm3shapes.so: cannot open shared
    object file").
  - Upstream fixed the install in `8a39c10`, and caelestia-shell 2.5.0 was
    released on r50.
  - With this archive the shell drew its bar, border and wallpaper, with no
    QML load error.
- Code at r38: 34 files, about 6,000 lines of C++ and QML, with no binaries
  and no submodules.
  - It includes only standard C++ and Qt Quick/QML headers.
  - It has no process execution, network, D-Bus, file or environment access.
  - It loads only its own compiled shaders, from Qt resources.
- The 12 commits from r38 to r50 (31 files, +354/-222) change:
  - the build: `qt_standard_project_setup`, GNUInstallDirs, and a CMake
    package config;
  - the headers, which move to `include/m3shapes` and are installed;
  - the C++ namespace and file names;
  - a Nix flake, and a stray PKGBUILD that is removed.

  A grep of the added lines finds no process, network or file code. The only
  URL is the flake's homepage. `CMakeLists.txt` has no FetchContent,
  ExternalProject, `execute_process` or download.
- Built with `makechrootpkg -c` in a clean chroot in the disposable development
  VM `rice-pkgs`. `.PKGINFO` and the file list match the recipe:
  - `libm3shapes.so` in `/usr/lib`;
  - the plugin, `m3shapes.qmltypes` and `qmldir` under
    `/usr/lib/qt6/qml/M3Shapes`, with the plugin's RUNPATH `/usr/lib`;
  - 14 headers under `/usr/include/m3shapes`;
  - the CMake package under `/usr/lib/cmake/M3Shapes`;
  - the license.

  No file is setuid or group-writable.
- License: Apache-2.0.
- Not done: Qt itself.
- Exact approved archive:
  `qt6-m3shapes-git-r50.8a6fe89-1-x86_64.pkg.tar.zst`, SHA-256
  `0d5a8577cea9160a4414ae92216608a676e8d5ff0160800cf1b3a68153f425ce`.
  This approval covers no other version, architecture, or build.
