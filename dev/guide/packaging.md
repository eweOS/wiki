---
title: Packaging Guideline
description: 
published: 1
date: 2023-10-19T06:18:57.198Z
tags: 
editor: markdown
dateCreated: 2023-02-13T14:12:50.481Z
---

eweOS' packaging is similar to Arch and other pacman-based distros. While most of the time you can refer to [Arch packaging guidelines](https://wiki.archlinux.org/title/Arch_package_guidelines), there are some caveats you need to know.

## Architectures

Unlike Arch Linux, which is a x86_64-only distro as for now, eweOS is a cross-platform distro. Therefore, the `arch` array should contain *the intersection* of all currently supported architectures `(x86_64 aarch64 riscv64)` *and* architectures the package itself supports, if the package is platform-dependent. Otherwise, use `arch=(any)`.

## Split packages

While we don't split packages as much as Debian does (for example, [their FFmpeg source package](https://packages.debian.org/source/sid/ffmpeg) produces both `lib<name><version>` and `lib<name>-dev` packages), we split packages according to functionality and best effort. For example, our `pacman` is split into 4 packages (`libalpm`, `pacman`, `makepkg` and `repo-tools`), each with distinct usage.

Another metric of splitting is its applicable architecture. `makepkg` and `repo-tools` are simply scripts, so they are marked `arch=(any)`

If one cannot decide to split or not, just leave it as one large package for now and discuss with eweOS developers.

## Checksums

This is already covered in Arch packaging guidelines. We re-emphasize:

> **Do not diminish the security or validity of a package** (e.g. by removing a checksum check or by removing PGP signature verification), because an upstream release is broken or suddenly lacks a certain feature (e.g. PGP signature missing for a new release)

