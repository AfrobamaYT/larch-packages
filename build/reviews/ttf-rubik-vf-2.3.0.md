# ttf-rubik-vf 2.3.0-3, any

- Upstream is `googlefonts/rubik`, archived since 2023. The recipe takes five
  files at `e337a5f69a9bea30e58d05bd40184d79cc099628` ("New binaries",
  2023-06-13), the head of `main`:
  - the two variable fonts `Rubik[wght].ttf` and `Rubik-Italic[wght].ttf`;
  - `OFL.txt`, `AUTHORS.txt` and `CONTRIBUTORS.txt`.

  All five SHA-256 values equal the recipe's pins; fresh downloads for this
  review and makepkg's own check both matched. Each file's git blob hash
  equals the entry in that commit's tree.
- The local PKGBUILD at `318a0024da34de008aa43ffe045ddeb6b6d77000` is the AUR
  recipe at `df5b264`, unchanged. It has no `build()`; `package()` only
  installs the files.
- The fonts are plain TrueType data:
  - 21 tables, and every table checksum is valid, as is the whole-file
    checksum;
  - no bytes after the last table;
  - one weight axis, 300-900;
  - no hinting programs beyond gftools' standard 7-byte `prep`, and no glyph
    instructions.

  They contain nothing executable.
- Built with `makechrootpkg -c` in a clean chroot in the disposable development
  VM `rice-pkgs`. The file list matches the recipe: the two fonts under
  `/usr/share/fonts/TTF` and the three texts under
  `/usr/share/licenses/ttf-rubik-vf`. makepkg keeps the URL encoding, so the
  fonts install as `Rubik%5Bwght%5D.ttf`; that is cosmetic, and fontconfig
  reads them by content.
- License: OFL-1.1.
- Not done: glyph and layout-table semantics (no FreeType or fontTools run).
- Exact approved archive:
  `ttf-rubik-vf-2.3.0-3-any.pkg.tar.zst`, SHA-256
  `394f6b0889b7744007daf4fc515e2b16092a4d50dc260b98af687d7be115022c`.
  This approval covers no other version, architecture, or build.
