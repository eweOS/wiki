---
title: GTK
description: 
published: 1
date: 2024-04-28T14:38:45.175Z
tags: 
editor: markdown
dateCreated: 2023-12-28T09:51:15.677Z
---

# C++ API

> Accroding to [gtk versioning style](https://blog.gtk.org/2016/09/01/versioning-and-long-term-stability-promise-in-gtk/), we usually use even minor (stable) versions.
{.is-info}


## Current version (GTK4)

- `libsigc++3` : Latest
- `glibmm` : Latest
- `cairomm` : Latest
- `pangomm` : Latest

## Previous version (GTK3)

- `libsigc++2` : Latest
- `glibmm-gtk3` : 2.66.6 (API 2.4)
- `cairomm-gtk3` : 1.14.5 (API 1.0)
- `pangomm-gtk3` : 2.46.3 (API 1.4)
- `atkmm` (no longer needed in GTK4): 2.28.3 (API 1.6)
- `gtkmm3` : Latest

# Troubleshoot

## Hardware Acceleration

Known issue: bad renders on `virtio-gpu` of qemu.
Solution:  `GSK_RENDERER=cairo`.