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
| ags-hyprpanel-git r630.1961ba8-2 | MIT | [commit 1961ba8](https://github.com/Jas-SinghFSU/HyprPanel/commit/1961ba86ad5ab880beb639e5454054b2b5037e0d) | `build/pkgbuilds/ags-hyprpanel-git`: the AUR recipe at a900623, with changes (see its review) |
| agsv1 1.9.0-3.1 | GPL-3.0-or-later and GPL-2.0-or-later | [commit 67b0e31](https://github.com/Aylur/ags/commit/67b0e31ded361934d78bddcfc01f8c3fcf781aad) (tag v1.9.0) | `build/pkgbuilds/agsv1`: kotontrion's own recipe (kotontrion/PKGBUILDS at 580117d, 0BSD), with changes (see its review) |
| appmenu-glib-translator-git 25.04.r11.ga783b01-1 | LGPL-3.0 | [commit a783b01](https://gitlab.com/vala-panel-project/vala-panel-appmenu/-/commit/a783b01c8b653349843fac9bbd075dac52cdc9de) | `build/pkgbuilds/appmenu-glib-translator-git`: the AUR recipe at 8586fa2, with changes (see its review) |
| aquamarine 0.15.1.1-2 | BSD-3-Clause | [tag v0.15.1](https://github.com/hyprwm/aquamarine/archive/v0.15.1/aquamarine-0.15.1.tar.gz), SHA-256 `2f9de98c…`, plus [commit fc77bd5](https://github.com/hyprwm/aquamarine/commit/fc77bd58a2c9ef6d0760a7c9c3b7b6670f956f28) | `build/pkgbuilds/aquamarine`: Arch's recipe at 33bf60a with that upstream fix and one change of Larch's own for nested headless screens (see its review) |
| arch-update 4.4.2-1 | GPL-3.0-or-later | [tag v4.4.2](https://github.com/Antiz96/arch-update/archive/v4.4.2.tar.gz), SHA-256 `c5d1af37…` | `build/pkgbuilds/arch-update`: the AUR recipe at 02244db, unchanged |
| avizo 1.3-1 | GPL-3.0-only | [commit 79367b2](https://github.com/misterdanb/avizo/commit/79367b2e363f4fb6235819d8e574d72d6e2f79e4) (tag 1.3), SHA-256 `2b1f5817…` | `build/pkgbuilds/avizo`: the AUR recipe at 16e8df6, unchanged |
| aylurs-gtk-shell 3.1.2-1 | GPL-3.0-only | [commit bbee2f1](https://github.com/Aylur/ags/commit/bbee2f18939f1ec7ff720e717cf305e73635628f) (tag v3.1.2), SHA-256 `7c9bf38c…` | `build/pkgbuilds/aylurs-gtk-shell`: the AUR recipe at 3d9e58d, with changes (see its review) |
| bibata-cursor-theme-bin 2.0.7-1 | GPL-3.0-or-later | [commit 35ccfe2](https://github.com/ful1e5/Bibata_Cursor/commit/35ccfe209a808e40d6c2ca60a46cbe4faf68b690) | `build/pkgbuilds/bibata-cursor-theme-bin`: the AUR recipe at 5d418e2, unchanged |
| caelestia-cli 1.1.3-1 | GPL-3.0 | [release v1.1.3: caelestia-1.1.3.tar.gz](https://github.com/caelestia-dots/cli/releases/download/v1.1.3/caelestia-1.1.3.tar.gz) | `build/pkgbuilds/caelestia-cli`: the AUR recipe at a6f5c17, unchanged |
| caelestia-shell 2.5.0-1.1 | GPL-3.0 | [release v2.5.0: caelestia-shell-v2.5.0.tar.gz](https://github.com/caelestia-dots/shell/releases/download/v2.5.0/caelestia-shell-v2.5.0.tar.gz) | `build/pkgbuilds/caelestia-shell`: the AUR recipe at d2c7b31, with changes (see its review) |
| catppuccin-cursors-mocha 2.0.0-1 | GPL-2.0 | [commit a7eb085](https://github.com/catppuccin/cursors/commit/a7eb08527dcce01010fa0ec46fa2bc4c3154f0d4) | `build/pkgbuilds/catppuccin-cursors-mocha`: the AUR recipe at 99c0102, unchanged |
| chwd 1.24.1-1 | GPL-3.0-or-later | [commit e99ec33](https://github.com/CachyOS/chwd/commit/e99ec339715f2b5724a1adc100ea55b94e59df5a) (tag 1.24.1) | `build/pkgbuilds/chwd`: CachyOS's recipe, source pinned, with Larch's graphics profiles |
| clipse 1.2.1-1 | MIT | [commit 95d666b](https://github.com/savedra1/clipse/commit/95d666b6cd8cbaec22732d605bc838365f144617) (tag v1.2.1) | `build/pkgbuilds/clipse`: the AUR recipe at 7760fcb, with changes (see its review) |
| darkly 0.5.39-2 | GPL-2.0-or-later and MIT (from Oxygen) | [commit 65f6fa6](https://github.com/Bali10050/darkly/commit/65f6fa62675e3c30986f8fc8e4fdbba053096491) (tag v0.5.39) | `build/pkgbuilds/darkly`: the AUR recipe at 204aad8, with changes (see its review) |
| elephant 2.22.1-1 | GPL-3.0 | [commit 8f1e21d](https://github.com/abenz1267/elephant/commit/8f1e21d6efe40b8b3953f95b9574f99f717caf91) (tag v2.22.1) | `build/pkgbuilds/elephant`: the upstream author's AUR recipe, unchanged |
| elephant-calc 2.22.1-1 | GPL-3.0 | [commit 8f1e21d](https://github.com/abenz1267/elephant/commit/8f1e21d6efe40b8b3953f95b9574f99f717caf91) (tag v2.22.1) | `build/pkgbuilds/elephant-calc`: the upstream author's AUR recipe, unchanged |
| elephant-desktopapplications 2.22.1-1 | GPL-3.0 | [commit 8f1e21d](https://github.com/abenz1267/elephant/commit/8f1e21d6efe40b8b3953f95b9574f99f717caf91) (tag v2.22.1) | `build/pkgbuilds/elephant-desktopapplications`: the upstream author's AUR recipe, unchanged |
| elephant-providerlist 2.22.1-1 | GPL-3.0 | [commit 8f1e21d](https://github.com/abenz1267/elephant/commit/8f1e21d6efe40b8b3953f95b9574f99f717caf91) (tag v2.22.1) | `build/pkgbuilds/elephant-providerlist`: the upstream author's AUR recipe, unchanged |
| elephant-websearch 2.22.1-1 | GPL-3.0 | [commit 8f1e21d](https://github.com/abenz1267/elephant/commit/8f1e21d6efe40b8b3953f95b9574f99f717caf91) (tag v2.22.1) | `build/pkgbuilds/elephant-websearch`: the upstream author's AUR recipe, unchanged |
| eww 0.6.0-1 | MIT | [commit d87c2fd](https://github.com/elkowar/eww/commit/d87c2fdbfdc012e76d229e4e9ea3325bc0f23e89) (tag v0.6.0) | `build/pkgbuilds/eww`: the AUR recipe at 756d212, unchanged |
| grimblast-git r168.57baf31-1 | MIT | [commit 57baf31](https://github.com/hyprwm/contrib/commit/57baf317e5196a8286b80976771ef55febad8660) | `build/pkgbuilds/grimblast-git`: the AUR recipe at a0e85f9, with changes (see its review) |
| hypr3d 0.5.0.r124.g632a523-1 | MIT; compiled in: Jolt (MIT), cgltf (MIT), stb_image (public domain); links cairo and pango | [commit 632a523](https://github.com/AfrobamaYT/Hypr3D/commit/632a5230ef8d11ac2c7f6646aa9354656339b197) of Larch's fork AfrobamaYT/Hypr3D: [samine825/Hypr3D](https://github.com/samine825/Hypr3D) d0be2e0 plus Larch's fixes (seven of them since taken upstream), one room across every monitor, a room that stays as it was left, a second avatar, the companion, for the AI teammate, with its eye, movement with weight, legible window text, F2 to read a window, F4 to show one big, portals to walk into, a menu on F1 that follows the player, a room drawn to the screen pixel for pixel, a room that closes when the session locks, a monitor wall that stands on the floor, a waste bin, soft shadows, drawing only on change, the rice's bar as a HUD, F7 to close or kill a window, objects and pictures at runtime, head tracking (off by default), a TV a window is put on and F8 to use it, colour-only materials no longer black, a view that stays on the monitor it was opened from, a window fullscreened on another monitor brought to the one in front, tiles handed back to the layout on leaving, Super+F a screen in front with the room around it, and the room's look after Larch's design drafts -- a crosshair that names what it points at, Larch's pointer, the windows lifting off their tiles into the room, portals as lit doors gone through into a starting panel, no physics debug asserts in the package (one crashed Hyprland), and Super + right drag resizing from a corner with the new size drawn in the room and a waste bin that catches a carried window by where the crosshair points, a fullscreen game fullscreen again after a visit to the room, no crash leaving the room after a window hid, and walking at the monitor's frame rate; SHA-256 `77e6b531…` | `build/pkgbuilds/hypr3d`: Larch's own recipe (see its reviews) |
| hyprland-preview-share-picker-git 0.2.1.r16.g0ef9b30-1 | MIT | [commit 0ef9b30](https://github.com/WhySoBad/hyprland-preview-share-picker/commit/0ef9b302aee716f36ea19e33ff3cc457d8c075a8) | `build/pkgbuilds/hyprland-preview-share-picker-git`: the AUR recipe at 1aa950b, source pinned, licence installed |
| hyprlang2lua 0.7.1-1 | MIT | [tag v0.7.1](https://github.com/EIonTusk/hyprlang2lua/archive/refs/tags/v0.7.1.tar.gz), SHA-256 `fa041a03…` | `build/pkgbuilds/hyprlang2lua`: the AUR recipe at 9a37482, unchanged |
| hyprlax 2.2.7-1 | MIT | [commit 6aaf881](https://github.com/sandwichfarm/hyprlax/commit/6aaf8814fcc6b729f59f6494df7655d6c45445f0) (tag v2.2.7) | `build/pkgbuilds/hyprlax`: the AUR recipe at 3207ce7, unchanged |
| hyprnotify 0.8.0-1 | Apache-2.0 | [commit 45d5ebd](https://github.com/codelif/hyprnotify/commit/45d5ebd416bfae5998700c17fa5affdccc90e376) (tag v0.8.0) | `build/pkgbuilds/hyprnotify`: the AUR recipe at 27d04e3, unchanged |
| hyprshade 5.0.0-1 | MIT | [commit 5195f8b](https://github.com/loqusion/hyprshade/commit/5195f8b84bf8fead4aa39c47785fc85b87a5746e) (tag 5.0.0), SHA-256 `4a102c34…` | `build/pkgbuilds/hyprshade`: the AUR recipe at 89c7100, unchanged |
| hyprswitch 5.0.0-1 | MIT | [commit 43d29cd](https://github.com/egnrse/hyprswitch/commit/43d29cda4acb4fa9bcd31c0dd58ee67a423445ea) (tag v5.0.0) | `build/pkgbuilds/hyprswitch`: the AUR recipe at b16c634, with changes (see its review) |
| lexend-fonts-git 1:r114.7894f02-2 | OFL-1.1 | [commit 7894f02](https://github.com/googlefonts/lexend/commit/7894f02b2e7eabc48595f1d4eff3b17b48c6e651) | `build/pkgbuilds/lexend-fonts-git`: the AUR recipe at adc286e, with changes (see its review) |
| libastal-4-git r986.cbcd9f4-1 | LGPL-2.1-only | [commit cbcd9f4](https://github.com/Aylur/astal/commit/cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e) | `build/pkgbuilds/libastal-4-git`: the AUR recipe at eb705bb, with changes (see its review) |
| libastal-battery-git r986.cbcd9f4-1 | LGPL-2.1-only | [commit cbcd9f4](https://github.com/Aylur/astal/commit/cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e) | `build/pkgbuilds/libastal-battery-git`: the AUR recipe at 1e0594e, with changes (see its review) |
| libastal-bluetooth-git r986.cbcd9f4-1 | LGPL-2.1-only | [commit cbcd9f4](https://github.com/Aylur/astal/commit/cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e) | `build/pkgbuilds/libastal-bluetooth-git`: the AUR recipe at 8ec78d9, with changes (see its review) |
| libastal-cava-git r986.cbcd9f4-1 | LGPL-2.1-only | [commit cbcd9f4](https://github.com/Aylur/astal/commit/cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e) | `build/pkgbuilds/libastal-cava-git`: the AUR recipe at 0005669, with changes (see its review) |
| libastal-git r986.cbcd9f4-1 | LGPL-2.1-only | [commit cbcd9f4](https://github.com/Aylur/astal/commit/cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e) | `build/pkgbuilds/libastal-git`: the AUR recipe at bc978b8, with changes (see its review) |
| libastal-gjs-git r986.cbcd9f4-1 | LGPL-2.1-only | [commit cbcd9f4](https://github.com/Aylur/astal/commit/cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e) | `build/pkgbuilds/libastal-gjs-git`: the AUR recipe at d818054, with changes (see its review) |
| libastal-hyprland-git r986.cbcd9f4-1 | LGPL-2.1-only | [commit cbcd9f4](https://github.com/Aylur/astal/commit/cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e) | `build/pkgbuilds/libastal-hyprland-git`: the AUR recipe at a9b5451, with changes (see its review) |
| libastal-io-git r986.cbcd9f4-1 | LGPL-2.1-only | [commit cbcd9f4](https://github.com/Aylur/astal/commit/cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e) | `build/pkgbuilds/libastal-io-git`: the AUR recipe at c02a8d9, with changes (see its review) |
| libastal-mpris-git r986.cbcd9f4-1 | LGPL-2.1-only | [commit cbcd9f4](https://github.com/Aylur/astal/commit/cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e) | `build/pkgbuilds/libastal-mpris-git`: the AUR recipe at 53495b5, with changes (see its review) |
| libastal-network-git r986.cbcd9f4-1 | LGPL-2.1-only | [commit cbcd9f4](https://github.com/Aylur/astal/commit/cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e) | `build/pkgbuilds/libastal-network-git`: the AUR recipe at c443158, with changes (see its review) |
| libastal-notifd-git r986.cbcd9f4-1 | LGPL-2.1-only | [commit cbcd9f4](https://github.com/Aylur/astal/commit/cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e) | `build/pkgbuilds/libastal-notifd-git`: the AUR recipe at caf9cc8, with changes (see its review) |
| libastal-powerprofiles-git r986.cbcd9f4-1 | LGPL-2.1-only | [commit cbcd9f4](https://github.com/Aylur/astal/commit/cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e) | `build/pkgbuilds/libastal-powerprofiles-git`: the AUR recipe at 09f36b6, with changes (see its review) |
| libastal-tray-git r986.cbcd9f4-1 | LGPL-2.1-only | [commit cbcd9f4](https://github.com/Aylur/astal/commit/cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e) | `build/pkgbuilds/libastal-tray-git`: the AUR recipe at ce2d085, with changes (see its review) |
| libastal-wireplumber-git r986.cbcd9f4-1 | LGPL-2.1-only | [commit cbcd9f4](https://github.com/Aylur/astal/commit/cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e) | `build/pkgbuilds/libastal-wireplumber-git`: the AUR recipe at b36e073, with changes (see its review) |
| libcava 1.0.0-1 | MIT | [tag 1.0.0](https://github.com/LukashonakV/cava/archive/1.0.0.tar.gz) | `build/pkgbuilds/libcava`: the AUR recipe at 3940344, unchanged |
| libinput-gestures 2.81-1 | GPL-3.0-or-later | [commit 9552f0d](https://github.com/bulletmark/libinput-gestures/commit/9552f0dd9b9e78e57840c58c0006e6519bb6e038) (tag 2.81) | `build/pkgbuilds/libinput-gestures`: the AUR recipe at 05c5bae, with changes (see its review) |
| ml4w-dotfiles-settings 2026.10.01-1 | GPL-3.0-only | [commit 9199d4b](https://github.com/mylinuxforwork/ml4w-dotfiles-settings/commit/9199d4b76fafce81fe68aab67ee8f29136e4ec6d), SHA-256 `e36ea3cc…` | `build/pkgbuilds/ml4w-dotfiles-settings`: Larch's own recipe; no AUR recipe exists (see its review) |
| mpvpaper 1.9-1 | GPL-3.0 | [commit 131a52c](https://github.com/GhostNaN/mpvpaper/commit/131a52c266d25262c62b85f52a4a978cafae6ee2) (tag 1.9) | `build/pkgbuilds/mpvpaper`: the AUR recipe at 722e4f1, unchanged |
| nm-tray 0.5.1-1 | GPL-2.0-or-later | [commit 1d55df4](https://github.com/palinek/nm-tray/commit/1d55df42144e06d0ace64740f433e04f2094e1dc) (tag 0.5.1) | `build/pkgbuilds/nm-tray`: the AUR recipe at b4fb13b, unchanged |
| papirus-folders 1.14.0-1 | MIT | [commit 0f838ee](https://github.com/PapirusDevelopmentTeam/papirus-folders/commit/0f838ee5679229e3a3e97e3b333c222c9e9615b4) (tag v1.14.0) | `build/pkgbuilds/papirus-folders`: the AUR recipe at 03b24dc, with changes (see its review) |
| paru 2.1.0-2 | GPL-3.0-or-later | [tag v2.1.0](https://github.com/Morganamilo/paru/archive/v2.1.0.tar.gz), SHA-256 `eea4dbb5…` | `build/pkgbuilds/paru`: the AUR recipe at 329be21, its alpm update pinned |
| piper-tts 1.8.0-1 | GPL-3.0-or-later and Apache-2.0 | [commit 639388b](https://github.com/OHF-Voice/piper1-gpl/commit/639388b6317fc4731e91d53da42aea68fd4166ff) (tag v1.8.0), plus espeak-ng [commit 724808c](https://github.com/espeak-ng/espeak-ng/commit/724808c5a83f9ef95fdd0db886ba7ba537ff224a) | `build/pkgbuilds/piper-tts`: the AUR recipe at e190a7c, with changes (see its review) |
| poweralertd 0.3.0-1 | GPL-3.0-only | [commit 2b54c64](https://git.sr.ht/~kennylevinsen/poweralertd/commit/2b54c6486b5dd73588a9626f3b211d2ace061fe8) (tag 0.3.0) | `build/pkgbuilds/poweralertd`: the AUR recipe at 3ede879, unchanged |
| pwvucontrol 0.5.3-2 | GPL-3.0-only (26 files say or-later) | [commit fd5c9d1](https://github.com/saivert/pwvucontrol/commit/fd5c9d1e5458b625d45e4159634b5b072f66cde1) (tag 0.5.3), SHA-256 `5ac6db39…` | `build/pkgbuilds/pwvucontrol`: the AUR recipe at 66ec831, with changes (see its review) |
| pyprland 3.4.4-1 | MIT | [commit acc4f39](https://github.com/hyprland-community/pyprland/commit/acc4f39b233e6f53d998b69fa01e6359746e3770) (tag 3.4.4), SHA-256 `5e9b695d…` | `build/pkgbuilds/pyprland`: the AUR recipe at 7ebb36e, with changes (see its review) |
| python-imageio-ffmpeg 0.6.0-2 | BSD-2-Clause | [commit ae47d80](https://github.com/imageio/imageio-ffmpeg/commit/ae47d8028c237ca5507ceef1b843ee427b442887) (tag v0.6.0) | `build/pkgbuilds/python-imageio-ffmpeg`: the AUR recipe at c9adcba, unchanged |
| python-materialyoucolor 3.0.2-1 | MIT | [tag v3.0.2](https://github.com/T-Dynamos/materialyoucolor-python/archive/v3.0.2.tar.gz) | `build/pkgbuilds/python-materialyoucolor`: the AUR recipe at 7a148d4, unchanged |
| python-pywal16 1:3.8.15-1 | MIT | [commit a04c3e3](https://github.com/eylles/pywal16/commit/a04c3e3b57ec57bdf080a863f45f917a18208e58) (tag 3.8.15), SHA-256 `cd3e4588…` | `build/pkgbuilds/python-pywal16`: the AUR recipe at d391e2c, unchanged |
| python-pywalfox 2.9.0-1 | MPL-2.0 | [commit 2622afa](https://github.com/Frewacom/pywalfox-native/commit/2622afac5995c96cc4db71c1ff9311308642cdbb) (tag v2.9.0) | `build/pkgbuilds/python-pywalfox`: the AUR recipe at af862b7, unchanged |
| python-screeninfo 0.8.1-2 | MIT and BSD-3-Clause | [commit 0cf3055](https://github.com/rr-/screeninfo/commit/0cf3055ccaf583a00a7a3a049f85a7c58dfd8884) (tag 0.8.1) | `build/pkgbuilds/python-screeninfo`: the AUR recipe at 358c408, unchanged |
| python-sherpa-onnx 1.13.8-1 | Apache-2.0, GPL-3.0-or-later, MIT, BSD-2-Clause, BSD-3-Clause and MPL-2.0 | [commit 11afbd0](https://github.com/k2-fsa/sherpa-onnx/commit/11afbd009a7f8c08f4bcf2fc1b265d0df4670fbf) (tag v1.13.8), SHA-256 `b0374cc5…`, and eleven dependency archives (see its review) | `build/pkgbuilds/python-sherpa-onnx`: the AUR recipe sherpa-onnx at 2fbfea7, with changes (see its review) |
| qt6-m3shapes-git r50.8a6fe89-1 | Apache-2.0 | [commit 8a6fe89](https://github.com/soramanew/m3shapes/commit/8a6fe8961749887d677700b6508e0c9249968b7e) | `build/pkgbuilds/qt6-m3shapes-git`: the AUR recipe at f4184f7, with changes (see its review) |
| qtengine 0.2.2-2 | BSD-2-Clause | [commit 167e7d9](https://github.com/kossLAN/qtengine/commit/167e7d9a27cdc8005ef2bd4d5d317b9da01b853f) (tag 0.2.2) | `build/pkgbuilds/qtengine`: the AUR recipe at 79a97c6, with changes (see its review) |
| quarrel-git r986.cbcd9f4-1 | LGPL-2.1-only | [commit cbcd9f4](https://github.com/Aylur/astal/commit/cbcd9f49dd6b9638dc5623b56cc6e1e0a60b593e) | `build/pkgbuilds/quarrel-git`: the AUR recipe at c5cf1fd, with changes (see its review) |
| rofi-power-menu 3.1.0-2 | MIT | [commit 395c1e0](https://github.com/jluttine/rofi-power-menu/commit/395c1e07360b2dbd13c0a658665ab0a581024ec3) (tag 3.1.0) | `build/pkgbuilds/rofi-power-menu`: the AUR recipe at 5e499fa, unchanged |
| runapp 0.5.1-1 | MIT | [commit 1ba272e](https://github.com/c4rlo/runapp/commit/1ba272ec2e7fbb7c7fd353283a2430dd5f704df2) (tag 0.5.1) | `build/pkgbuilds/runapp`: the upstream author's AUR recipe, with changes (see its review) |
| shim-signed 16.1+fedora+7-1 | BSD-2-Clause | [Fedora's shim 16.1-7](https://koji.fedoraproject.org/koji/packageinfo?packageID=14502), prebuilt and signed by Microsoft; x86_64 RPM SHA-512 `642f7bd6…` | `build/pkgbuilds/shim-signed`: the AUR recipe at 2fb92b9, unchanged |
| sunsetr 0.12.5-1 | MIT | [commit 3261a3a](https://github.com/psi4j/sunsetr/commit/3261a3a9bbebcd866cb1da2825aee80904f3f495) (tag v0.12.5) | `build/pkgbuilds/sunsetr`: the AUR recipe at 201dc38, unchanged |
| swaylock-effects 1.7.0.0-4 | MIT | [commit 4f2234c](https://github.com/jirutka/swaylock-effects/commit/4f2234c6bca3ce80dce1dbf7407825a38d58103c) (tag v1.7.0.0), SHA-256 `e94d79e1…` | `build/pkgbuilds/swaylock-effects`: the AUR recipe at c614e0b, unchanged |
| tofi 0.9.1-2 | MIT | [commit 71a4801](https://github.com/philj56/tofi/commit/71a4801d20d8904cfcfa5e92c96d53ee06a2c69f) (tag v0.9.1) | `build/pkgbuilds/tofi`: the AUR recipe at 0ee27a5, unchanged |
| ttf-go 2.010-2 | BSD-3-Clause | [commit ffcb3fe](https://github.com/golang/image/commit/ffcb3fe7d1bf4ed2e01a95a552bb3b7f5dab24d1) (tag v0.1.0) | `build/pkgbuilds/ttf-go`: the AUR recipe at 21a42ca, unchanged |
| ttf-rubik-vf 2.3.0-3 | OFL-1.1 | [commit e337a5f](https://github.com/googlefonts/rubik/commit/e337a5f69a9bea30e58d05bd40184d79cc099628) | `build/pkgbuilds/ttf-rubik-vf`: the AUR recipe at df5b264, unchanged |
| walker 2.17.1-2 | GPL-3.0 | [commit 56c9e2b](https://github.com/abenz1267/walker/commit/56c9e2b69e7d2b00f0f9481ae8c89f53810c1de5) (tag v2.17.1) | `build/pkgbuilds/walker`: the upstream author's AUR recipe, with changes (see its review) |
| waybar-module-pacman-updates-git 0.2.14-1 | GPL-3.0-or-later | [commit bc77269](https://github.com/coffebar/waybar-module-pacman-updates/commit/bc772692928bee1a7aa5778af6ab65d34e93abab) | `build/pkgbuilds/waybar-module-pacman-updates-git`: the AUR recipe at b52f7f1, with changes (see its review) |
| waypaper 2.9-1 | GPL-3.0-only | [commit 7c1f0b3](https://github.com/anufrievroman/waypaper/commit/7c1f0b3db4e666533822c2682b7ad42373ff18e8) (tag 2.9), SHA-256 `372c40c8…` | `build/pkgbuilds/waypaper`: the AUR recipe at 3dcfc55, unchanged |
| wl-clipboard-history-git r12.25bacd3-1 | MIT | [commit 25bacd3](https://github.com/janza/wl-clipboard-history/commit/25bacd3fd752ca02d316beb0bb16b8468da4f6a0) | `build/pkgbuilds/wl-clipboard-history-git`: the AUR recipe at 32a74ad, with changes (see its review) |
| wleave 0.7.1-2 | MIT | [commit 37e7cac](https://github.com/AMNatty/wleave/commit/37e7cace1b30022f09465eace3f6298be6869ac1) | `build/pkgbuilds/wleave`: the AUR recipe at 923e200, with changes (see its review) |
| wlogout 1.2.2-0 | MIT | [release 1.2.2: wlogout.tar.gz](https://github.com/ArtsyMacaw/wlogout/releases/download/1.2.2/wlogout.tar.gz) | `build/pkgbuilds/wlogout`: the AUR recipe at 9904ef2, unchanged |
| workstyle-git 0.9.0.r146.gdae1501-1 | MIT | [commit dae1501](https://github.com/pierrechevalier83/workstyle/commit/dae15018c84c4f0feaf498d3676271ca0e3bec44) | `build/pkgbuilds/workstyle-git`: the AUR recipe at adfe61b, with changes (see its review) |

For the packages under the GPL or LGPL this is their Corresponding Source: the upstream source above
together with the recipe here that builds it, with `makechrootpkg -c` in a clean chroot. Build
dependencies are fetched at the versions each project's lock file pins; for paru, its recipe pins
the alpm crate on top. The full hashes are in the review records. The recipes are exact copies of the commit each package was built from
(`recipe_commit` in `build/approved-packages.json`, a commit of Larch's repository).

Recipes taken from the AUR or from CachyOS keep their origin's terms; Larch's own recipes and
changes are GPL-3.0-or-later (`LICENSE`).
