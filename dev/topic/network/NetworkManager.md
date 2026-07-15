---
title: NetworkManager
description: 
published: 1
date: 2026-07-15T09:12:51.352Z
tags: 
editor: markdown
dateCreated: 2025-01-31T17:38:13.370Z
---

# NetworkManager

NetworkManager is a *standard Linux network configuration tool suite* and has been a default option in many distros.

## Installation

```shell
sudo pacman -Sy networkmanager

# Install auto-config scripts for 
# NetworkManager in cloud
sudo pacman -Sy nm-cloud-setup
```

To start NM at boot time, do:

```shell
sudo dinitctl enable networkmanager
```

---

Additionally, `ethtool` is also *recommended* to install:

```shell
sudo pacman -Sy ethtool
```

Without this tool, the script `mdev-helper-settle-nics` in package `busybox` may misbehave, resulting in unexpected network interface names.

See also: [The commit in packages/busybox](https://github.com/eweOS/packages/commit/570d860717f0b86bb5c84140fa6b8e7002287520)

## Note

it is possible that you might run into issue where `connman` or any other service may conflict with `NetworkManager` in that case make sure any other network managing service isn't running

To check run

```shell
sudo dinitctl list
```

if you see anything like `connman` running firstly stop and disable it and then start `NetworkManager`

## Status

WIP.

NetworkManager in eweOS currently ignores all device probe events otherwise won't manage any network interfaces. This is due to the missing hotplugging ability in [libudev-zero](https://github.com/illiliti/libudev-zero). For detailed info see [this closed PR](https://github.com/eweOS/packages/pull/2983).

