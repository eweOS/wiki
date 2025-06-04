---
title: Guideline for Writing pkgdesc
description: 
published: 1
date: 2025-06-04T13:35:33.100Z
tags: 
editor: markdown
dateCreated: 2025-06-04T13:35:33.099Z
---

# Guideline for Writing pkgdesc

It has been found that our pkgdesc entries are messy in format and some of them don't provide effective information or are too redundant. This documentation serves as a guideline for clear, informative, and precise pkgdescs.

## Use a full sentence

The description should be a full sentence starting with an UPPERCASE letter.

### BAD

> stacking wayland compositor with look and feel from openbox.

### GOOD

> Stacking wayland compositor with look and feel from openbox

## Avoid trailing periods

Although it's a full sentence, pkgdesc appears in places where trailing periods look redundant or unnatural, for example,

```
$ pacman -Si ctags
Repository      : main
Name            : ctags
Version         : 6.1.20250511.0-2
Description     : A maintained ctags implementation.
Architecture    : x86_64
URL             : https://github.com/universal-c1tags/ctags
Licenses        : GPL-2.0-or-later
Groups          : None
Provides        : None
Depends On      : libseccomp  jansson  libyaml  libxml2
Optional Deps   : None
Conflicts With  : None
Replaces        : None
Download Size   : 740.26 KiB
Installed Size  : 1973.02 KiB
Packager        : eweos-x8664-worker1
                  <eweos-x8664-worker1@workers.os-build.ewe.moe>
Build Date      : Mon May 19 03:24:37 2025
Validated By    : MD5 Sum  SHA-256 Sum  Signature
```

Description becomes the only item that comes with trailing punctuaction.

## Be descriptive instead of definition

Descriptions are meant to provide an overview of the package. Please make sure one hasn't heard of the package is able to understand its purpose from the description.

### BAD

> Buildtool package set

### GOOD

> Basic, default toolset for building eweOS packages

pkgdesc shouldn't be an A.D. for the project.

### BAD

> An extremely fast hash algorithm

### GOOD

> A fast, non-cryptographic hash algorithm.


## About the Documentation

It used to be an RFC which could be found at [this GitHub issue](https://github.com/eweOS/packages/issues/4036).

During drafting,

- [AOSC packaging style](https://wiki.aosc.io/developer/packaging/package-styling-manual/)

is taken as reference.