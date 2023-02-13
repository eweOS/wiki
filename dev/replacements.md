---
title: Software Replacements
description: 
published: 1
date: 2023-02-13T13:44:00.363Z
tags: 
editor: markdown
dateCreated: 2023-02-11T16:47:39.341Z
---

# Software Replacements

Some softwares are replaced in eweOS. Here is a incomplete list.

## Replaced

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
- `systemd-tmpfiles` : `pawprint`
- `systemd-sysuser` : `catnest`
- `systemd-logind` : `seatd`
- `systemd-dbus` : `basu`

## Work in progress

- `readline` : `libedit`

## Rejected

- `openssl` : `libressl`. It's too hard to maintain sets of patches for unsupported packages.
- `dbus` : `dbus-broker`. It needs libsystemd for dbus-launcher.

## Unsupported

### Clang C++23

- `hyprland`
- `btop`

### musl functions

### busybox features

### other reasons