---
title: Network
description: 
published: 1
date: 2024-04-29T12:53:46.322Z
tags: 
editor: markdown
dateCreated: 2024-04-29T12:50:02.597Z
---

eweOS currently provides `connman` and `ifupdown-ng` as network managers.

## ifupdown-ng

Provides by package `ifupdown-ng`. To make it start at boot time, enable dinit service `ifupdown-ng`

For wifi support, package `wpa_supplicant` should be installed.

## connman

Provides by package `connman`. To make it start at boot time, enable dinit service `connman`

Wireless is supported and included in dependencies.

To manage network, use `sudo connmanctl`.