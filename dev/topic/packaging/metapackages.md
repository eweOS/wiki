---
title: Meta Packages
description: 
published: 1
date: 2024-10-05T14:42:17.088Z
tags: 
editor: markdown
dateCreated: 2024-10-05T14:42:17.088Z
---

The most important meta package is `base`, which provides

- basic runtime libraries (`musl` `llvm-libs`)
- shell (`bash`)
- basic command line utils (`busybox` `util-linux`)
- package manager (`pacman`)
- [filesystem structure](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard) (`filesystem`)

combining into a working rootfs and suits for chrooting, but is never enough for a normal eweOS installation.

Other important meta packages are

- `base-baremetal`: Packages suitable for a baremetal/VM installation
- `base-devel`: Common development-purpose packages
- `base-container`: Packages suitable for a container installation (WIP)

# FAQ

- Differing from Arch Linux, `base` on eweOS doesn't contain a service manager and corresponding service description. `dinit` should be installed manually along with `dinit-services` or `dinit-services-container`(WIP).
- Kernels (`linux` and `linux-lts`) are optional dependencies of `base-baremetal`.