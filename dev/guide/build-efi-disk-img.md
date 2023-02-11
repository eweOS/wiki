---
title: Build EFI Disk Image
description: 
published: 1
date: 2023-02-11T16:55:10.288Z
tags: 
editor: markdown
dateCreated: 2023-02-11T16:55:10.288Z
---

# Build Bootable EFI Disk Image {.tabset}

## Use prebuilt KIS

You may need `efistub-bin` from `testing`.

```
#!/bin/bash

IMAGE=eweOS-testbuild-x86_64-efi-$(date -Idate).qcow2
LODEV=/dev/nbd0
DISKIMAGE=eweOS-rollingrelease.x86_64-1.1.0

echo "Downloading data..."

rm eweOS-rollingrelease*

wget -r -l1 --no-parent -A ".xz" --no-directories https://os-repo.ewe.moe/eweos-images/x86_64/

tar xvf eweOS-rollingrelease.*

rm ./*.xz

echo "Cleaning env..."

sudo umount ./mnt/boot || true
sudo umount ./mnt/ || true

rm ./*.img
rm $IMAGE

echo "Creating disk..."

qemu-img create -f qcow2 -o compression_type=zstd -o preallocation=metadata $IMAGE 50G

sudo modprobe nbd || true

sudo qemu-nbd -f qcow2 -c $LODEV $IMAGE

(
echo g
echo n
echo 1
echo  
echo +256M
echo t
echo 1
echo n
echo 2
echo  
echo  
echo w
) | sudo fdisk $LODEV

echo "Setting up loop device..."

SYSDEV=${LODEV}p2
BOOTDEV=${LODEV}p1

echo "Formatting loop device..."

sudo mkfs.ext4 ${SYSDEV}  -O "-metadata_csum_seed -orphan_file"
sudo e2label ${SYSDEV} EWE_ROOT
sudo mkfs.fat -F 32 ${BOOTDEV}

echo "Making mountpoint..."

mkdir -p ./mnt
sudo mount ${SYSDEV} ./mnt
sudo mkdir -p ./mnt/boot
sudo mount ${BOOTDEV} ./mnt/boot

echo "Installing system..."
mkdir -p ./mnt-img
sudo mount $DISKIMAGE ./mnt-img
cd ./mnt-img
sudo rsync -avxHAX --progress ./ ../mnt
cd ..
sudo umount ./mnt-img

echo "Setting up system..."

sudo pacman --noconfirm -r ./mnt -U efistub-bin-0.1.0-1-x86_64.pkg.tar.gz
sudo mkdir -p ./mnt/boot/EFI/BOOT
sudo cp ./mnt/usr/lib/efistub/BOOTX64.EFI ./mnt/boot/EFI/BOOT/BOOTX64.EFI

sleep 2

echo "Umounting loop devices..."

sudo umount ./mnt/boot
sudo umount ./mnt
sudo qemu-nbd -d $LODEV

echo "Compressing qcow2 file"

mv $IMAGE $IMAGE.old
qemu-img convert -c -O $IMAGE $IMAGE
rm $IMAGE.old
```

## Pacstrap from Archlinux

> WIP