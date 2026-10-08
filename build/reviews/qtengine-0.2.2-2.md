# qtengine 0.2.2-2, x86_64

- What it is: qtengine 0.2.2-1 (see qtengine-0.2.2.md) rebuilt from the same
  source and recipe against Qt 6.12; only `pkgrel` and a header comment
  differ in the recipe at `ead0a386`. The same nine files as 0.2.2-1.
- Why: the system upgrade of 2026-10-08 03:49 brought Qt 6.12.0. The 0.2.2-1
  platform theme plugin, built against 6.11, still loaded but supplied no
  icon theme: with `QT_QPA_PLATFORMTHEME=qtengine`, as caelestia's shell
  runs, Quickshell resolved none of `preferences-system-network`,
  `network-wired`, `brave-browser` or `image-missing`; the owner saw the
  launcher's theme icons as pink-black squares.
- Built with `tools/larch-packages build qtengine` in the clean chroot
  (qt6-base 6.12.0-2 there, per `.BUILDINFO`); `.BUILDINFO` records the
  committed PKGBUILD's SHA-256 `4271ed6803a5...`, which matches.
- Measured on the owner's PC, read-only (a Quickshell probe shell with no
  window, `QT_QPA_PLATFORM=wayland`, the new plugin first on
  `QT_PLUGIN_PATH`): all four icons resolve, as with
  `QS_ICON_THEME=Papirus-Dark`; with the installed 0.2.2-1 none.
  `basecamp` resolves with neither: no icon of that name exists.
- License: unchanged.
- Exact approved archive: `qtengine-0.2.2-2-x86_64.pkg.tar.zst`, SHA-256
  `b394d38bb5742cd40153a0adaa8b9081d2f2c2d673856e70b5ce37b4eead7e0a`.
  This approval covers no other version or build; it replaces the approval
  of 0.2.2-1.
