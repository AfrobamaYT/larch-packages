# shim-signed 16.1+fedora+7-1, any

- Provenance: the AUR recipe at `2fb92b90a7b8` (2026-07-31, maintainer
  nl6720), unchanged. It downloads Fedora's build of
  shim 16.1-7 from kojipkgs.fedoraproject.org; the x86_64 RPM's SHA-512
  `642f7bd6...777e218f0` equals the recipe's (measured 2026-10-02). That
  commit went back from 16.1-8 (2026-06-11) to 16.1-7 without saying why.
- Authenticity is Microsoft's signature, not the download: `shimx64.efi`
  carries two, "Microsoft Corporation UEFI CA 2011" and "Microsoft UEFI CA
  2023", so it starts on firmware that knows either. OVMF with Microsoft's
  keys (`virt-fw-vars --enroll-microsoft`) started it with Secure Boot on.
  `mmx64.efi` (MokManager) is signed by Fedora's key, which shim carries
  (`.vendor_cert`).
- Capabilities: binaries only; nothing runs at installation, the `.install`
  file only prints a warning about SBAT (read). shim starts `grubx64.efi` from its own directory after
  checking it against the firmware's db, the MOK list and its vendor
  certificate, and starts MokManager when a MOK request is pending; under
  Secure Boot it also checks what that second stage loads (measured: a
  MOK-signed EFI image started, an unsigned one was refused).
- Needed by: `larch-secure-boot` (Secure Boot on the factory keys).
- Revocation: Microsoft's SBAT and dbx updates retire old shims; when Windows
  Update applies one, only a newer shim starts. This package has to follow
  Fedora's releases.
- License: BSD-2-Clause.
- Built with `tools/larch-packages build shim-signed` from the recipe at
  `528833c8` in the clean chroot (devtools); its `.BUILDINFO` records that
  PKGBUILD's SHA-256 `b89b470d...`. The archive holds the six EFI files under
  /usr/share/shim-signed, 0644 and root's, nothing else; `shimx64.efi` and
  `mmx64.efi` are byte for byte the ones in Fedora's RPM.
- Exact approved archive:
  `shim-signed-16.1+fedora+7-1-any.pkg.tar.zst`, SHA-256
  `a3e4af2ba6f97000c12d5081e5dccf7800e4735140557010481512f738c0ac64`.
  This approval covers no other version or build.
