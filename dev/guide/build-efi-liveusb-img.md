---
title: Build EFI LiveUSB Image
description: 
published: 1
date: 2023-02-26T16:28:01.377Z
tags: 
editor: markdown
dateCreated: 2023-02-26T16:28:01.377Z
---

You may need `BOOTX64.EFI` from `efistub-live-bin` in `testing` repo.

```
#!/bin/bash

IMAGE=eweOS-live-testbuild-x86_64-efi-$(date -Idate).img
SFSIMAGE=eweOS-rollingrelease.x86_64-1.4.0-SquashFS-Build53.1.squashfs

echo "[STEP] Downloading data..."

if [[ ! -f "$SFSIMAGE" ]]
then
	wget https://os-repo.ewe.moe/eweos-images/x86_64/$SFSIMAGE.xz
	xz -d $SFSIMAGE.xz
fi

echo "[STEP] Cleaning env..."

sudo umount ./mnt/boot 2>/dev/null || true
sudo umount ./mnt/ 2>/dev/null || true

rm $IMAGE 2>/dev/null
rm $IMAGE.xz 2>/dev/null
rm $IMAGE.xz.sha256 2>/dev/null

echo "[STEP] Creating disk..."

dd if=/dev/zero of=$IMAGE bs=1M count=128
LODEV=`sudo losetup -P -f --show $IMAGE`
(
echo g
echo n
echo 1
echo  
echo +16M
echo t
echo 1
echo n
echo 2
echo  
echo  
echo w
) | sudo fdisk $LODEV

SYSDEV=${LODEV}p2
BOOTDEV=${LODEV}p1

echo "[STEP] Formatting loop device..."

sudo mkfs.ext4 -q ${SYSDEV}
sudo e2label ${SYSDEV} EWE_ROOT
sudo mkfs.fat -F 16 ${BOOTDEV}

echo "[STEP] Making mountpoint..."

mkdir -p ./mnt
sudo mount ${SYSDEV} ./mnt
sudo mkdir -p ./mnt/boot
sudo mount ${BOOTDEV} ./mnt/boot

echo "[STEP] Setting up system..."

sudo mkdir -p ./mnt/boot/EFI/BOOT
sudo cp ./BOOTX64.EFI ./mnt/boot/EFI/BOOT/BOOTX64.EFI
sudo cp ./$SFSIMAGE ./mnt/ewe.sfs

echo "[STEP] Umounting loop devices..."

sudo umount ./mnt/boot
sudo umount ./mnt
sudo losetup -d $LODEV

echo "[STEP] Compressing image file"

exit

xz -T0 $IMAGE

sha256sum $IMAGE.xz | cut -d ' ' -f 1 > $IMAGE.xz.sha256sum
```