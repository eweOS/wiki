---
title: Bootloader
description: 
published: 1
date: 2025-08-12T03:51:57.599Z
tags: 
editor: markdown
dateCreated: 2023-02-26T16:25:19.855Z
---

> **BIOS Boot is not officially supported anymore**
> eweOS only support UEFI bootloaders. There may be some packages supporting BIOS booting but they're not officially supported.
{.is-warning}


# limine

We use [`limine`](/dev/topic/sysutils/limine) as replacement for `grub`. It is the default bootloader for eweOS.

## Installation

```
pacman -S limine
```

Install limine and create corresponding boot entry.

```
limine-install --efi-directory=EFI_PARTITION_MOUNTPOINT TARGET_DEVICE
```

For firmware that doesn't support setting [EFI variable](https://uefi.org/specs/UEFI/2.10/08_Services_Runtime_Services.html) at runtime (e.g. [U-Boot](https://docs.u-boot.org/en/latest/develop/uefi/uefi.html#performing-the-update)), or only looks for removable boot paths (in particular some MSI boards, this is a firmware bug!), it may be necessary to install the bootloader in removable mode.

```
limine-install --removable --efi-directory=EFI_PARTITION_MOUNTPOINT
```

Note that for each storage device, there's only one bootloader that may be installed as removable. Please make sure this doesn't override your other bootloader configuration before running this command.

Generate limine configuration

```
limine-mkconfig -o EFI_PARTITION_MOUNTPOINT/limine.conf
```

Currently kernel updating and initramfs generation is handled by `limine-mkconfig` as well, so running `limine-mkconfig` (without arguments) may be needed after a system upgrade or changing initramfs configuration.

`limine-mkconfig` would only read kernels located at `/usr/lib/modules/` AND belongs to packages installed by pacman. Single user mode menu options will also be generated.