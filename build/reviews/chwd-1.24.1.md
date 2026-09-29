# chwd 1.24.1-1, x86_64

- Upstream source is the fixed CachyOS commit
  `e99ec339715f2b5724a1adc100ea55b94e59df5a` (tag `1.24.1`).
  The local recipe at `f6a207ba71e90156e4f3f36614046959ab68b0ee`
  packages only `chwd`, its upstream Lua hook runner and Larch's graphics
  profiles. Its local profile SHA-256 is pinned to
  `0821da25d6c90d9cdda734482686d826bf02db7923bf88e6cc15fcc4e9564196`.
- The profile hooks execute shell commands as root by design. The shipped
  profile file is root-owned when installed. Its reviewed hooks manage
  graphics packages, driver configuration, services and initramfs; they
  contain no download-and-execute command. The hook runner quotes package
  names passed to pacman. The shipped hook script SHA-256
  `dbb6760e8f23a1d2efd4cff1e4e5641d02600c54c1168922635cef897cd49a12`
  matched upstream source byte for byte.
- Built in the disposable `chwd-review` VM after the profile hash check.
  `cargo test --locked` passed 25 tests. Installing the package and running
  `chwd -a` selected the QEMU profile, installed its Arch packages, recorded
  the installed profile and created `/etc/mkinitcpio.conf.d/10-chwd-qemu.conf`.
  NVIDIA hardware paths were not run on physical hardware by this review.
- Exact approved archive:
  `chwd-1.24.1-1-x86_64.pkg.tar.zst`, SHA-256
  `25ab6827c1814865dbe619c47de76f0ac2b9305d885c9bb27f5876d05cc9c1f9`.
  This approval covers no other build.
