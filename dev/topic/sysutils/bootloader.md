---
title: Bootloader
description: 
published: 1
date: 2024-09-09T16:28:25.227Z
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
limine-install EFI_PARTITION_MOUNTPOINT
```

Generate limine configuration

```
limine-mkconfig -o EFI_PARTITION_MOUNTPOINT/limine.conf
```

Currently kernel updating and initramfs generation is handled by `limine-mkconfig` as well, so running `limine-mkconfig` (without arguments) may be needed after a system upgrade or changing initramfs configuration. 

`limine-mkconfig` would only read kernels located at `/usr/lib/modules/` AND belongs to packages installed by pacman. Single user mode menu options will also be generated.