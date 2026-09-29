# larch-packages

The pacman repository `[larch]` of [Larch](https://github.com/AfrobamaYT/Larch). It carries only
packages that were reviewed one by one: every exact archive has a review record in `build/reviews/`
and its SHA-256 in `build/approved-packages.json`, and it is signed by Larch's package key.
Everything else comes from Arch's repositories or, after the person's own review, from the AUR.

Packages are published as assets of the `x86_64` release. Larch's installer adds the repository;
by hand:

```
[larch]
SigLevel = Required
Server = https://github.com/AfrobamaYT/larch-packages/releases/download/$arch
```

and trust the signing key (`larch-packages.asc` in the release):

```
sudo pacman-key --add larch-packages.asc
sudo pacman-key --lsign-key 608A3BA47440E661754A42FB83E3280B2639ADB8
```

The keys `3DCFF6FC8F8C1770CA40B9C4078F4A946BDA4207` and `B596953AF87CB754E6807D3FE37F4729EB425C02`
are retired. If you trusted either, remove it: `sudo pacman-key --delete <fingerprint>`.

## Packages and their source

| Package | Licence | Upstream source | Recipe and its origin |
|---|---|---|---|
| paru 2.1.0-2 | GPL-3.0-or-later | [tag v2.1.0](https://github.com/Morganamilo/paru/archive/v2.1.0.tar.gz), SHA-256 `eea4dbb5…` | `build/pkgbuilds/paru`: the AUR recipe at 329be21, its alpm update pinned |
| arch-update 4.4.2-1 | GPL-3.0-or-later | [tag v4.4.2](https://github.com/Antiz96/arch-update/archive/v4.4.2.tar.gz), SHA-256 `c5d1af37…` | `build/pkgbuilds/arch-update`: the AUR recipe at 02244db, unchanged |
| chwd 1.24.1-1 | GPL-3.0-or-later | [commit e99ec33](https://github.com/CachyOS/chwd/commit/e99ec339715f2b5724a1adc100ea55b94e59df5a) (tag 1.24.1) | `build/pkgbuilds/chwd`: CachyOS's recipe, source pinned, with Larch's graphics profiles |
| hyprlang2lua 0.7.1-1 | MIT | [tag v0.7.1](https://github.com/EIonTusk/hyprlang2lua/archive/refs/tags/v0.7.1.tar.gz), SHA-256 `fa041a03…` | `build/pkgbuilds/hyprlang2lua`: the AUR recipe at 9a37482, unchanged |
| hyprland-preview-share-picker-git 0.2.1.r16.g0ef9b30-1 | MIT | [commit 0ef9b30](https://github.com/WhySoBad/hyprland-preview-share-picker/commit/0ef9b302aee716f36ea19e33ff3cc457d8c075a8) | `build/pkgbuilds/hyprland-preview-share-picker-git`: the AUR recipe at 1aa950b, source pinned, licence installed |

For the GPL-3.0-or-later packages this is their Corresponding Source: the upstream source above
together with the recipe here that builds it, with `makechrootpkg -c` in a clean chroot. Build
dependencies are fetched at the versions each project's lock file pins; for paru, its recipe pins
the alpm crate on top. The full hashes are in the review records. The recipes are exact copies of the commit each package was built from
(`recipe_commit` in `build/approved-packages.json`, a commit of Larch's repository).

Recipes taken from the AUR or from CachyOS keep their origin's terms; Larch's own recipes and
changes are GPL-3.0-or-later (`LICENSE`).
