# Quick Notes

## Packages

### busybox

- ~~remove `halt` `poweroff` `reboot` for `dinit`~~ (Finished)
- ~~remove `lspci` for `pciutils`~~ (Finished)
- ~~enable `ash` for initramfs~~ (Finished)

### mkinitramfs

- ~~remove `bash`~~ (Finished)
- ~~replace `bash` and `sh` with `ash`~~ (Finished)

### utmps

- A patch is introduced (`compat-path.patch`) to add additional defines to allow build of dinit. (Note)

### sudo

- Can be compiled with utmps.h

### mold

- Can be compiled with external `tbb`

### grub

- ~~EFI support requires `objcopy` from `binutils`, consider alternatives.~~ (`binutils-objcopy` is available now)
- ~~pxe.h is lost~~ (Fixed)
- Package split: `grub-common` `grub-bios` `grub-efi` `grub-theme-*`

### clover-efi

- Deprecate when EFI is support in grub.

### aria2

- test failed, also on arch, skipped check
- a service file can be add, although not on arch.

### binutils again

- Now `binutils-objcopy` is included to build GRUB-efi
- `binutils-gold` is under consideration

## Package Alternatives

- `glibc` : `musl`
- `gcc` `gcc-libs` : `clang` `llvm` `llvm-libs`
- `libtool` : `slibtool`
- `binutils` : `llvm`
- `coreutils` : `busybox`
- `util-linux` : `busybox` (partially)
- `kmod` : `busybox`
- `systemd` : `dinit`
- `lld` : `mold` (default)
- `zlib` : `zlib-ng`
- `libudev` : `libudev-zero`

### Work in progress

- `readline` : `libedit`

### Not considered

- `openssl` : `libressl`. It's too hard to maintain sets of patches for unsupported packages.

## Architecture

Currently: x86_64

Roadmap: arm64 riscv64 (as Tier-1 support)

- ~~`mold` have no riscv64 support yet.~~ (Now supported)