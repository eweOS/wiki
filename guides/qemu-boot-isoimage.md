---
title: Boot ISO Image from QEMU
description: Launch prebuilt eweOS iso images from QEMU
published: 1
date: 2025-01-23T18:49:32.845Z
tags: 
editor: markdown
dateCreated: 2024-04-29T08:43:11.737Z
---

## Download Image

### Architectures

Currently, only `x86_64` and `aarch64` are supported for iso images.

### Download ISO Images

ISO images can be downloaded from any accessable mirror in [Download](https://os.ewe.moe/download) page of eweOS.

For auto redirection for optimized mirrors, [https://os-repo-auto.ewe.moe/eweos-images/](https://os-repo-auto.ewe.moe/eweos-images/) is recommended.

Daily build images can be downloaded from [GitHub Actions](https://github.com/eweOS/iso/actions).

### Image Variants

- `liveimage-desktop`: Live ISO image with desktop environment configured to provide out-of-box experiment.
- `liveimage-minimal`: Live ISO image with cli tools only.
- `tarball`: Tarball of eweOS minimal system.

## Configure and boot Your VM

The following script can be used to boot eweOS, with hardware graphic acceleration.

```
#!/bin/bash

IMAGE=eweos-x86_64-liveimage-desktop.iso

# Adjust cpu and ram here!
VCPU=4
VRAM=4G

qemu-system-x86_64 \
    -smp $VCPU -m $VRAM -cpu host \
    -machine type=q35,accel=kvm \
    -cdrom $IMAGE \
    -device virtio-net,netdev=ewe -netdev user,id=ewe \
    -drive if=pflash,format=raw,readonly=on,file=/usr/share/OVMF/OVMF_CODE.fd \
    -device virtio-vga-gl -display gtk,gl=on \
    -device virtio-sound-pci,audiodev=eweaudio -audiodev alsa,id=eweaudio \
    -device qemu-xhci,id=xhci \
    -device usb-tablet,bus=xhci.0 \
    -device usb-kbd,bus=xhci.0
```

## Usage

The default username and password for eweOS iso image is `ewe:ewe`. For desktop mode ISO images, autologin is enabled.