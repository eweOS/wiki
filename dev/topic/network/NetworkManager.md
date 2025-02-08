---
title: NetworkManager
description: 
published: 1
date: 2025-02-08T17:04:38.717Z
tags: 
editor: markdown
dateCreated: 2025-01-31T17:38:13.370Z
---

# NetworkManager

NetworkManager is a *standard Linux network configuration tool suite* and has been a default option in many distros.

Status: WIP.

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

To avoid causing some problems, `ethtool` is also **recommended** to install:

```shell
sudo pacman -Sy ethtool
```

See also: [The commit in packages/busybox](https://github.com/JulianDroske/eweos-packages/commit/d85c42a47ed2e81d6b5f4df06de3f464bfb3f6f1)


## Status

WIP.

NetworkManager in eweOS currently ignores all device probe events otherwise won't manage any network interfaces. This is due to the missing hotplugging ability in [libudev-zero](https://github.com/illiliti/libudev-zero). For detailed info see [this closed PR](https://github.com/eweOS/packages/pull/2983).

