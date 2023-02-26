---
title: Boot Disk Image with QEMU
description: Guide to boot prebuilt disk image with QEMU
published: 1
date: 2023-02-26T16:19:18.419Z
tags: 
editor: markdown
dateCreated: 2023-02-24T12:44:30.352Z
---

# Download Image

## Architectures

Currently, only `x86_64` is supported for disk images.

## Download qcow2 (bootable virtual disk) Images

qcow2 images can be downloaded from any accessable mirror in [Download](https://os.ewe.moe/download) page of eweOS.

There are three files in a bundle:

- `eweOS-{RELEASE_TYPE}.{ARCH}-{VERSION}-{IMAGE_TYPE}-Build{BUILD_CODE}.qcow2`
	- qcow2 image, compressed with zstd.
- `eweOS-{RELEASE_TYPE}.{ARCH}-{VERSION}-{IMAGE_TYPE}-Build{BUILD_CODE}.qcow2.sha256`
  - sha256 checksum
- `eweOS-{RELEASE_TYPE}.{ARCH}-{VERSION}-{IMAGE_TYPE}-Build{BUILD_CODE}.packages`
  - A list of installed packages

# Configure and boot Your VM

The following script can be used to boot eweOS, with hardware graphic acceleration and EFI boot support.

```
#!/bin/bash

IMAGE=eweOS-{RELEASE_TYPE}.{ARCH}-{VERSION}-{IMAGE_TYPE}-Build{BUILD_CODE}.qcow2

VCPU=8
VRAM=4G

qemu-system-x86_64 \
	-smp $VCPU -m $VRAM -cpu host \
	-machine type=q35,accel=kvm \
  -hda $IMAGE \
	-device virtio-net,netdev=ewe -netdev user,id=ewe \
	-drive if=pflash,format=raw,readonly=on,file=/usr/share/edk2-ovmf/x64/OVMF_CODE.fd \
	-device virtio-vga-gl \
	-display gtk,gl=on
```

# Usage

The default username and password for eweOS disk image is `ewe:ewe`