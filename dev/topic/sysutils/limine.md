---
title: Limine
description: 
published: 1
date: 2024-09-09T16:51:47.233Z
tags: 
editor: markdown
dateCreated: 2024-09-09T16:51:47.233Z
---

Limine is an advanced, portable, multiprotocol bootloader, which is the default bootloader for eweOS.

Limine is provided by `limine` package on eweOS.

# Installation

## By `limine-install`

`limine-install` is a script to simplify installation of Limine, works just like `grub-install`. To use it, make sure `efibootmgr` is installed on your system (already listed as `limine`'s optional dependency) or boot entries cannot be created automatically.

Assuming your EFI partition is mounted on `/boot`, you could install Limine with

```
limine-install /boot
```

Some firmwares are picky (and not following the UEFI specification) with bootloader paths. Or `limine-install` may fail to create a boot entry on your machine. In these cases, try running `limine-install` with `--removable` argument, installing Limine in removable mode.

## Manually

UEFI-mode Limine is a PE executable file, located at `/usr/share/limine/`. Filename varies on different architectures, on `x86_64` it is `BOOTX64.EFI`. Copy it to `EFI_MOUNTPOINT/EFI/BOOT`.

## Install for Legacy BIOS mode (unsupported)

TODO

# Configuration

`limine-mkconfig` generates Limine configuration automatically. Configuration path should be specified with `-o`, like

```
limine-mkconfig -o /boot/limine.conf
```

(Limine after 8.0.0 uses `limine.conf` as default configuration name)

For now, other booting related work like kernel installation and initramfs generation is also handled by `limine-mkconfig`. So you should run it after a kernel upgrade or similar scenarios.