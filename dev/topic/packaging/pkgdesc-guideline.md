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

It has been found that our pkgdesc entries are messy in format and some of them do not provide effective information or are too redundant. This documentation serves as a guideline for clear, informative, and precise pkgdescs.

## Use a full sentence

The description should be a full sentence starting with an UPPERCASE letter, but with NO trailing periods.

### BAD

> stacking wayland compositor with look and feel from openbox.

### GOOD

> Stacking wayland compositor with look and feel from openbox

since pkgdesc appears in places where trailing periods look redundant or unnatural, for example,

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

where the description becomes the only item that comes with trailing punctuaction.

## More descriptive, less definitive

Descriptions are expected to provide a brief overview of a package, so that most people can understand the purpose of it from the description with little prior knowledge.

### BAD

> Buildtool package set

### GOOD

> Basic, default toolset for building eweOS packages

## Be neutral

A pkgdesc should not be an advertisement for the project.

Therefore, try not to use biased phrases which could make it less objective. Take an example for `zstd`:

### BAD

> Extremely fast, efficient and robust compression algorithm

### GOOD

> Fast real-time compression algorithm

while the word `extremely` contains strong emotion,  `efficient` and `robust` draw positive opinion on it, they are not ideal options.


## About the Documentation

It used to be an RFC which could be found at [this GitHub issue](https://github.com/eweOS/packages/issues/4036).

During drafting, the [AOSC packaging style](https://wiki.aosc.io/developer/packaging/package-styling-manual/) is taken as a reference.