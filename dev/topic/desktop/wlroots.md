---
title: wlroots
description: 
published: 1
date: 2024-09-09T16:20:39.681Z
tags: 
editor: markdown
dateCreated: 2024-01-19T08:46:33.172Z
---

`wlroots` is a modular wayland compositor library to ease development of compositors, which is used by [sway](/dev/topic/desktop/sway), [cage](/dev/topic/desktop/cage) and [wayfire](/dev/top/desktop/wayfrei).

eweOS ships different version of wlroots library, as wlroots does not provide API compatibility.

Each version of wlroots is split into two packages, library and development package. For example, `wlroots0.17` (library) and `wlroots0.17-devel` (development).

Library packages coexist, since there is only a dynamic library and soversion is bumped on a new release. Headers of different `wlroots` version are located at the same path, making coexistence of development packages require a lot of downstream work, so development packages are simply in conflict and cannot be installed at the same time.

## For package maintainers

- ALWAYS specify the exact `wlroots` version in `PKGBUILD`. `wlroots` is no longer provided.
- Add corresponding `wlroots` development package to `makedepends` in your `PKGBUILD`