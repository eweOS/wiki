---
title: Build EFI Disk Image
description: 
published: 1
date: 2023-02-16T22:33:39.542Z
tags: 
editor: markdown
dateCreated: 2023-02-13T14:12:45.490Z
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

wget -r -l1 --no-parent -A ".xz" --no-directories http://repo.nia.dn42/eweos-images/x86_64/

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
qemu-img convert -c -O qcow2 $IMAGE.old $IMAGE
rm $IMAGE.old
```

## Pacstrap from Archlinux

### Setting up rootfs

Firstly, create an empty raw image, format as ext4, and mount it on a directory.

```
$ dd if=/dev/zero of=eweos-testing.img bs=1M count=8172
$ mkfs.ext4 eweos-testing.img
$ mkdir eweos
# mount eweos-testing.img eweos
```

If you are not preparing for booting inside qemu, you can also simply use

```
$ mkdir eweos
# mount --bind eweos eweos
```

Then, install necessary packages. Get [a usable pacman.conf](https://os-repo.ewe.moe/eweos/pacman.conf) first.

Assuming that you already saved it as pacman.conf,

```
# pacstrap -C pacman.conf eweos base ca-certs
```

Also get a copy of resolv.conf,

```
$ cp /etc/resolv.conf eweos/etc/resolv.conf
```

Now chroot into this working rootfs of eweos. 

If you are using Arch Linux, install arch-install-scripts and

```
# arch-chroot eweos
```

Otherwise see [Using chroot](https://wiki.archlinux.org/title/Chroot#Using_chroot) for equivalent operations.

Inside the chroot container, set the password of root

```
# passwd
```

### Setting up inside qemu

Firstly inside the chroot container you've created, install several needed packages:

```
# pacman -Sy linux linux-headers dinit mkinitramfs
```

Make a initrd,

```
# mkinitramfs
```

Then copy generated /tmp/initrd.gz out of eweos chroot (without exiting it!). Also copy /usr/lib/modules/(The version of kernel)/vmlinux outside. If you already have qemu-system installed, issue (save as a shell script for convenience)

```
qemu-system-x86_64 -nographic \                 # Delete this if you want connecting over VNC
                   --enable-kvm \
                   -kernel vmlinux \            # The vmlinux file
                   -initrd initrd.gz \          # The initrd file
                   -m 4G \                      # The memory given to qemu virtual machine
                   -hda eweos-testing.img \     # The image we've created
                   -append "root=/dev/sda console=ttyS0" \
                   -nic user,model=virtio-net-pci
```

After login into the system, you need to manually set up the network,

```
# modprobe virtio-net
# ifconfig eth0 up
# udhcpc
```
