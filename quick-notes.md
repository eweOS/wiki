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
- ~~Package split: `grub-common` `grub-bios` `grub-efi` `grub-theme-*`~~ (Finished)
- EFI installation requires `efibootmanager`
- Add custom theme, maybe `grub-theme-eweos`?
- Remove `GNU/Linux` text from bootmenu
- Add initrd/vmlinuz search options for booster (patch from archlinux)

### clover-efi

- Deprecate when EFI is support in grub.

### aria2

- test failed, also on arch, skipped check
- a service file can be add, although not on arch.

### binutils again

- Now `binutils-objcopy` is included to build GRUB-efi
- `binutils-gold` is under consideration

### filesystem

- Add more groups

### dinit

- Add system groups/users for extra packages

### seatd

- ~~Seems not support clang 15~~ (Fixed)

### weston

- Can not enter graphic interface, maybe mesa problem?

## Package Alternatives

- `glibc` : `musl`
- `gcc` `gcc-libs` : `clang` `llvm` `llvm-libs`
- `libtool` : `slibtool`
- `binutils` : `llvm` + `binutils-*` (standalone tools)
- `coreutils` : `busybox`
- `util-linux` : `busybox` (partially)
- `kmod` : `busybox`
- `systemd` : `dinit`
- `lld` : `mold` (default)
- `zlib` : `zlib-ng`
- `libudev` : `libudev-zero`

### Work in progress

- `readline` : `libedit`
- `systemd-logind` : (`elogind` or `seatd`) with `libseatd`

### Not considered

- `openssl` : `libressl`. It's too hard to maintain sets of patches for unsupported packages.
- `dbus` : `dbus-broker`. It needs `libsystemd` for `dbus-launcher`.

## Architecture

Currently: x86_64

Roadmap: arm64 riscv64 (as Tier-1 support)

- ~~`mold` have no riscv64 support yet.~~ (Now supported)