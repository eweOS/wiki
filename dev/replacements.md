---
title: Software Replacements
description: Lists and status of alternatives we used in eweOS and a list of unsupported and dropped softwares
published: 1
date: 2023-12-07T03:49:06.209Z
tags: 
editor: markdown
dateCreated: 2023-02-13T14:12:40.309Z
---

Some softwares are replaced/dropped in eweOS. Here is a incomplete list.

## Dropped

- `polkit` (maybe?)

## Replaced

- `x11` : `wayland`
- `glibc` : `musl`
- `gcc` `gcc-libs` : `clang` `llvm` `llvm-libs`
- `libtool` : `slibtool`
- `binutils` : `llvm` + `binutils-*` (standalone tools)
- `coreutils` : `busybox`
- `util-linux` : `busybox` (partially)
- `kmod` : `busybox`
- `systemd` : `dinit`
- `lld` : `mold` (default)
- `zlib` : `zlib-ng` (Builtin multithreading may cause test failures)
- `libudev` : `libudev-zero`
- `systemd-tmpfiles` : `pawprint`
- `systemd-sysuser` : `catnest`
- `systemd-logind` : `seatd` `elogind`
- `systemd-dbus` : `basu`
- `oss` `pulseaudio` `jack` `alsa`(partially) : `pipewire` `wireplumber`
- `iptable` : `nftable`

## Work in progress

- `readline` : `libedit`

## Rejected

- `openssl` : `libressl`. It's too hard to maintain sets of patches for unsupported packages.
- `dbus` : `dbus-broker`. It needs libsystemd for dbus-launcher.

## Unsupported

### musl functions

### busybox features

- `dracut` (Missing features from GNU `coreutils`)

### requires X11

- `gnome` (building `mutter` without X11 is still WIP)
- `plasma` (building `plasma-framework` without X11 is still WIP)
- `xfce4` (x11 is required)
- `alacritty` (needs xcb)

### other reasons