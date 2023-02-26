---
title: Quick Notes
description: 
published: 1
date: 2023-02-26T21:22:27.267Z
tags: 
editor: markdown
dateCreated: 2023-02-13T14:12:34.727Z
---

### binutils-objcopy
- Failed to run on `aarch64`: `can't set BFD default target to `elf64-x86-64': invalid bfd target`

### mimalloc
- LD_PRELOAD test before linking by default

### llvm-lto
- Enable lto by default

### rust
- ~~Make sure `RUSTFLAGS='-C target-feature=-crt-static'` is added.~~ (Added)

### pacman
- Function: auto copy LICENSE

### libglvnd
- Provides `egl`

### python
- Can not upgrade to 3.11.1: triplet detection error with musl
- Split `setuptools` and `pip`

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
- `segfault` when using `awk`/`diff` in `riscv64`

### mkinitramfs

- ~~remove `bash`~~ (Finished)
- ~~replace `bash` and `sh` with `ash`~~ (Finished)

### utmps

- A patch is introduced (`compat-path.patch`) to add additional defines to allow build of dinit. (Note)
- `tty2socket` : replace `s6-ipcserverd` (~~under development~~ ~~finished~~ ~~more compatbile features needed~~ finally finished)
  - `IPCREMOTEEUID` must be set
- ~~Still not work, no socket connection~~
  - Packages must be compiled with `-lutmps` to use `utmps` features\
  - considering combining with musl itself

### mold

- Can be compiled with external `tbb`
- ~~libLLVM-gold LTO causes segfault~~ (Fixed)

### grub

- ~~EFI support requires `objcopy` from `binutils`, consider alternatives.~~ (`binutils-objcopy` is available now)
- ~~pxe.h is lost~~ (Fixed)
- ~~Package split: `grub-common` `grub-bios` `grub-efi` `grub-theme-*`~~ (Finished)
- ~~EFI installation requires `efibootmanager`~~ (Finished)
- Add custom theme, maybe `grub-theme-eweos`?
- Remove `GNU/Linux` text from bootmenu

### efivar

- ~~segfault, effected: `grub` `efibootmgr`~~ (Fixed)

### aria2

- test failed, also on arch, skipped check
- a service file can be add, although not on arch.

### binutils again

- Now `binutils-objcopy` is included to build GRUB-efi
- ~~`binutils-gold` is under consideration~~
- `binutils-gold` is included

### dinit

- ~~Add system groups/users for extra packages~~ (Finished by `opensysusers`)
- Restruct target services

### seatd

- ~~Seems not support clang 15~~ (Fixed)
- ~~`SIGSEGV` when starting (child process killed after `recvfrom` json)~~ (Fixed)

### pam

- Add to `base` group