---
title: Boot ISO Image from QEMU
description: 
published: 1
date: 2024-04-29T08:43:11.737Z
tags: 
editor: markdown
dateCreated: 2024-04-29T08:43:11.737Z
---

## Download Image

### Architectures

Currently, only `x86_64` and `aarch64` is supported for iso images.

### Download iso Images

iso images can be downloaded from any accessable mirror in [Download](https://os.ewe.moe/download) page of eweOS.

## Configure and boot Your VM

The following script can be used to boot eweOS, with hardware graphic acceleration and EFI boot support.

```
#!/bin/bash

IMAGE=eweos-x86_64-liveimage-desktop.iso

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

The default username and password for eweOS iso image is `ewe:ewe`