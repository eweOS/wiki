---
title: Bootloader
description: 
published: 1
date: 2024-04-29T08:45:12.620Z
tags: 
editor: markdown
dateCreated: 2023-02-26T16:25:19.855Z
---

> **BIOS Boot is not officially supported anymore**
> eweOS only support UEFI bootloaders. There may be some packages supporting BIOS booting but they're not officially supported.
{.is-warning}


# limine

We use `limine` as replacement for `grub`. It is the default bootloader for eweOS.

## Install

Install `limine`:

```
pacman -S limine
```

Install limine as default system EFI bootloader:

```
cp /usr/share/limine/BOOT{X64,AA64,RISCV64}.EFI /boot/EFI/BOOT/
```

## Config

```
limine-mkconfig > /boot/limine.cfg
```

`limine-mkconfig` would only read kernels located at `/usr/lib/modules/` AND belongs to packages installed by pacman. Single user mode menu options will also be generated.
