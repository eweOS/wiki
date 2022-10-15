# Quick Notes

## Packages

### python-kiwi (Build Env)
- Do not try `xz -l` to detect file info of a raw disk image, it costs too much time.

### mandoc
- use standard less as manpager (requiring replace busybox)         

### krb5, cyrus-sasl, openldap
- write service file
- implement .sysusers .tmpfiles

### busybox

- ~~remove `halt` `poweroff` `reboot` for `dinit`~~ (Finished)
- ~~remove `lspci` for `pciutils`~~ (Finished)
- ~~enable `ash` for initramfs~~ (Finished)
- add depmod script to run after installing modules (see [kmod PKGBUILD](https://github.com/archlinux/svntogit-packages/blob/packages/kmod/trunk/depmod-search.conf))

### mkinitramfs

- ~~remove `bash`~~ (Finished)
- ~~replace `bash` and `sh` with `ash`~~ (Finished)

### utmps

- A patch is introduced (`compat-path.patch`) to add additional defines to allow build of dinit. (Note)
- `tty2socket` : replace `s6-ipcserverd` (~~under development~~ ~~finished~~ more compatbile features needed)
  - `IPCREMOTEEUID` must be set
- Still not work, no socket connection
  - Packages must be compiled with `-lutmps` to use `utmps` features\
  - considering combining with musl itself

### mold

- Can be compiled with external `tbb`

### grub

- ~~EFI support requires `objcopy` from `binutils`, consider alternatives.~~ (`binutils-objcopy` is available now)
- ~~pxe.h is lost~~ (Fixed)
- ~~Package split: `grub-common` `grub-bios` `grub-efi` `grub-theme-*`~~ (Finished)
- ~~EFI installation requires `efibootmanager`~~ (Finished)
- Add custom theme, maybe `grub-theme-eweos`?
- Remove `GNU/Linux` text from bootmenu
- Add initrd/vmlinuz search options for booster (patch from archlinux)

### efivar

- segfault, effected: `grub` `efibootmgr`

### clover-efi

- Deprecate when EFI is support in grub.

### aria2

- test failed, also on arch, skipped check
- a service file can be add, although not on arch.

### binutils again

- Now `binutils-objcopy` is included to build GRUB-efi
- ~~`binutils-gold` is under consideration~~
- `binutils-gold` is included

### filesystem

- Add more groups

### dinit

- ~~Add system groups/users for extra packages~~ (Finished by `opensysusers`)

### seatd

- ~~Seems not support clang 15~~ (Fixed)
- `SIGSEGV` when starting (child process killed after `recvfrom` json)

### weston

- Can not enter graphic interface (without use `pixman` software backend), maybe mesa problem?

### pam

- Add to `base` group

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
- `systemd-sysuser` : `opensysusers` (substitution is under development)
- ~~`systemd-tmpfiles`~~ : `pawprint`, seems to work well

### Not considered

- `openssl` : `libressl`. It's too hard to maintain sets of patches for unsupported packages.
- `dbus` : `dbus-broker`. It needs `libsystemd` for `dbus-launcher`.

## Graphical Interface

Currently works:

- `weston`
  - Can launch via pixman (software render)
  - Can not launch without pixman

Currently not works:

- `sway` need pango and more gnome stuff
- ~~Mouse has offset in Proxmox, do not have event in QEMU~~ (Fixed)

## Architecture

Currently: x86_64

Roadmap: arm64 riscv64 (as Tier-1 support)

- ~~`mold` have no riscv64 support yet.~~ (Now supported)
- Need more infra for other archs!!!