# larch-packages

The pacman repository `[larch]` of [Larch](https://github.com/AfrobamaYT/Larch): AUR packages that
Larch's rices use, built in a clean chroot (aurutils + devtools) and signed, so a rice installs them
instead of compiling them on your machine.

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
sudo pacman-key --lsign-key 3DCFF6FC8F8C1770CA40B9C4078F4A946BDA4207
```

Built by `tools/larch-packages` in the Larch repository from `build/larch-packages.list`. Packages
whose licences forbid redistribution are not here; Larch builds those locally.
