---
title: Installation Guide (Manual)
description: 
published: 1
date: 2026-01-27T15:27:56.392Z
tags: 
editor: markdown
dateCreated: 2026-01-27T15:24:37.315Z
---

# eweOS Installation Guide (Manual)

This page aims to provide an overview of eweOS' manual installation process. Serving as a brief guide, it is impossible to cover all possible caveats you may meet during installation, please also refer to links provided in the section if you get confused/stuck with a step.

eweOS' wiki is still under heavy development, in case of issues uncovered by this site, please also consider search through,

- [ArchWiki](https://wiki.archlinux.org/)
- [Gentoo Wiki](https://wiki.gentoo.org)

## About the Automatic Installer

eweOS has a [port of Jade installer](https://github.com/eweOS/jade), providing functionality of installing eweOS through CLI or GUI, and could be installed from repository (package `jade` and `jade-gui`).

However, this installer has been unmaintained for some time due to lack of manpower. ***Use it at your own risk, it isn't supported anymore**.*

A guide to install eweOS with Jade through CLI is available [here](./jade-installation-guide).

## Prepare Live Medium

The usual installation process is done in a portable environment, called `Live`, which could be flashed into removable medium, and boots on bare-metal machines.

### Acquire a Live Image

You could browse a list of eweOS mirrors at [download page](https://os.ewe.moe/download), and click `Browse Images` (CD Icon) for image file lists. Selecting a nearby mirror may improve the downloading speed.

The images are crafted with different flavours,

- `tarball`: Compressed rootfs tarball, couldn't boot, not used in this installation guide.
- `standard`: ISO image, basic Live environment without GUI. Hardware firmware included.
- `desktop-xfce`: ISO image, full Live environment with Xfce desktop environment and GUI applications. Hardware firmware included.

and for all architectures supported by eweOS,

- `x86_64`, `aarch64`, `loongarch64`: `standard`, and `desktop-xfce` images are available.
- `riscv64`: Only `standard` image is available.

Please choose the image with architecture corresponding to your target machine. If you don't understand what architecture is, `x86_64` is probably the correct answer.

After downloading the image, it's recommended to verify its checksum. You could download the checksum file, which ends up with `.sha256`, from your selected mirror.

### Create a Live Medium

You could choose any storage devices to write the Live image: ISO images shipped by eweOS are hybird ones, which means it could be written to and boot from either hard drive or CD/DVD-ROM. However, ***writing Live images to a medium will wipe away all data from it, please choose one without important data, or back data up ahead.***

The image could be written to hard drives directly with `dd`. We don't recommend tools like `Rufus`, which may mess up partition labels and cause boot failures. If you have to use such tools, please select `DD mode`.

Ventoy [1.1.00](https://github.com/ventoy/Ventoy/releases/tag/v1.1.00) or later supports booting eweOS ISOs.

### Boot into Live Environment

You should plug your Live medium to the target machine, and set boot option to it. Please refer to your machine/mainboard's manual for exact instructions to do so.

If everything is correct, you should be able to boot into eweOS' bootloader menu, please choose your preferred option and press enter to boot it. For standard ISO users, it should be `eweOS Rolling (LiveCD)`, suffixed with kernel versions varying among ISO versions.

For desktop ISO users, there are multiple profiles to choose,

- `Live Desktop`: Desktop environment with GUI.
- `Live CLI with Framebuffer Term`: Similar to `Live CLI`, but enables`fbterm` for correctly rendering CJK characters.
- `Live CLI`: Command-line only environment, providing similar experience to `standard` image flavour.
- corresponding "low-memory" profiles: doesn't copy rootfs to memory, suitable for machines with less than 4GiB memory.

eweOS Live environment runs in memory by default, which causes a higher memory usage. This should be okay for CLI-only profiles, but users with less than 4GiB memory may fail to boot into `Live Desktop`, in which case error messages like

```
!> unable to copy squashfs, insufficient memory?
```

may display. Please consider "low-memory" profiles if it happens.

## Setup Live Environment

### Configure Network

The Live environment doesn't provide full set of packages to complete the installation, thus it's necessary to configure network to download them.

#### With NetworkManager

This option only works in `Live Desktop`-flavoured image, since package `networkmanager` isn't shipped in other images.

NetworkManager provides an interactive `TUI` configuration program, which could be invoked with `nmtui`.

#### Manual Configuration 

First, bring the interface up,

```shell
ip link set <INTERFACE> up
```

For wireless connection, you need to configure and invoke `wpa_supplicant` to authenticate and connect to the AP. ArchWiki provides a [hand-by-hand guide](https://wiki.archlinux.org/title/Wpa_supplicant).

`wpa_supplicant` supports many different configuration options, for a detailed view, please refer to its [documentation](https://git.w1.fi/cgit/hostap/plain/wpa_supplicant/README) and [configuration example](https://git.w1.fi/cgit/hostap/tree/wpa_supplicant/wpa_supplicant.conf). After successful authentication and association, you should observe dmesg like

```
wlan0: authenticate with 11:45:14:51:19:19 (local address=19:19:81:01:14:51)
wlan0: send auth to 11:45:14:51:19:19 (try 1/3)
wlan0: authenticated
wlan0: associate with 11:45:14:51:19:19 (try 1/3)
wlan0: RX AssocResp from 11:45:14:51:19:19 (capab=0x1111 status=0 aid=2)
wlan0: associated
wlan0: Limiting TX power to 30 (30 - 0) dBm as advertised by 11:45:14:51:19:19
```

And then you should configure IP for the interface. This could be done with `udhcpc` when DHCP is available. You could simply invoke it with interface as argument,

```shell
udhcpc -i <INTERFACE>
```

### Select eweOS Mirror

eweOS' package manager, pacman, uses the mirror specified in `/etc/pacman.d/mirrorlist` by default.

The default configuration takes `https://os-repo-auto.ewe.moe` as repository, which redirects you to the nearest mirror, but doesn't work all the time. Please consider switch to a mirror nearby by comment `https://os-repo-auto.ewe.moe` and uncomment another mirror in the file, if downloading is too slow or fails too often.

## Install Target System

Now the Live environment is ready, it's time to install eweOS.

### Partition the Target Disk

You could partition the target disk with `fdisk` command, which is part of `util-linux` package, and shipped in all variants of Live images. A guide of its usage could be found on [ArchWiki](https://wiki.archlinux.org/title/Fdisk)

It's recommended to create one FAT32 partition more than 512MiB for ESP if you don't have one already, and one EXT4/BtrFS/XFS partition for root directory. A clean minimal eweOS installation usually takes less than 2GiB, but you'll need more space for root directory if you want to install additional packages or to store more data.

It's suggested to have ESP mounted as `/boot`: eweOS' default bootloader, Limine, recognizes only FAT-family filesystems, thus putting kernel image and initramfs in the ESP could avoid the burden of creating a separate partition for `/boot`. Mounting ESP as `/boot` is the only partitioning schema officially supported by eweOS' Limine helper scripts for now.

After paritioning the disk, the partitions must be formatted to contain a filesystem. Different packages should be installed, depending on your filesystem type,

- FAT-family: `mkfs.fat`/`mkfs.vfat` (aliases to the same tool), provided by `dosfstools`.
- EXT-family: `mkfs.ext2`, `mkfs.ext3`, and `mkfs.ext4`, provided by `e2fsprogs`
- BtrFS: `mkfs.btrfs`, provided by `btrfs-progs`
- XFS: `mkfs.xfs`, provided by `xfsprogs`

### Install eweOS Rootfs

Every basic eweOS installation should contain `base` package. For bare-metal installation, it's also recommended to install `base-baremetal` to pull in packages like `tinyramfs` (for generation of initramfs), `dinit-services` (system services), and `limine` (the bootloader).

However, `base-baremetal` doesn't automatically pull in a kernel package, and you should manually specify one to install. eweOS maintains two kernel packages: `linux` is the latest stable kernel, and `linux-lts` is the latest LTS kernel.

Before installing the rootfs, you should have the partition for it mounted somewhere.

#### With pacstrap

`pacstrap` is provided by `arch-install-scripts` package.

```shell
pacstrap <ROOT_MOUNTPOINT> base base-baremetal linux [OTHER PACKAGES]
```

You could run `pacstrap --help` for a detailed list of possible options.

#### With pacman

The data directory for `pacman` must be created manually ahead of time,

```shell
mkdir -p <ROOT_MOUNTPOINT>/var/lib/pacman
```

then run `pacman` with

```shell
pacman --root <ROOT_MOUNTPOINT> -Syu base base-baremetal linux [OTHER PACKAGES]
```

Differing from `pacstrap`, pacman doesn't automatically copy mirror configuration from Live environment to the target rootfs. Please configure them manually again if it's necessary.

## Configure Target System

Now an eweOS copy has been installed on your target disk. However to make it fully functional and bootable, some configuration must be done.

### Enter the Target System

Please install package `arch-install-scripts` for `arch-chroot script`, then run

```shell
arch-chroot <ROOT_MOUNTPOINT>
```

In the new shell poped after running the command, `/` is the rootfs partition that you've installed eweOS, instead of the Live environment. It's important to remember which system you're making changes to.

### Configure /etc/fstab

This file records mapping between mountpoint and block device, its detailed format is described on [ArchWiki](https://wiki.archlinux.org/title/Fstab). In a word, you should configure fstab entries for your `/boot` and root directory, which usually looks like,

```fstab
# Static information about the filesystems.
# See fstab(5) for details.

# <file system>                                  <dir> <type> <options> <dump> <pass>
UUID=44C1-5BD9                                   /boot   vfat    rw      0       1
UUID=0a8f578b-102a-485a-8ed8-bf267bdd5fa5        /       ext4    rw      0       1
```

It's recommended to use `PARTUUID` and `UUID` instead of device path to identify block devices. Block device path isn't stable between boots, e.g., on systems with two SCSI disks, `/dev/sda` doesn't always refer to the same disk among different boots. It's also possible to unintentionally cause similar situations, for example, having a USB stick plugged during booting of a system with one SATA disk.

### Configure Initramfs

`tinyramfs` is the default tool for generating initramfs on eweOS. Its configuration locates at `/etc/tinyramfs/config`. Usually these options are essential,

- `root`: Block device for root directory. Similar to fstab's case, it's recommended to use `UUID` or `PARTUUID` here.
- `rootfs_type`: Filesystem type for root directory, like `ext4`, `btrfs`, `xfs`.
- `compress`: Command used to compress the initrd, should read data from stdin and write compressed data to stdout, e.g., `gzip -9`

You could find a commented list of tinyramfs options at `/usr/share/tinyramfs/config.example.conf`. Manpage `tinyramfs(5)` provides a detailed description of their behavior.

### Install and Configure Bootloader

Before installation of Limine, please install `efibootmgr` for `limine-install` to set efivars up with eweOS' boot option.

[Here](https://os-wiki.ewe.moe/dev/topic/sysutils/limine) is a detailed guide for installation and configuration of Limine bootloader. In a word, invoking `limine-install` and `limine-mkconfig` works for most machines,

```shell
# Assuming ESP is mounted as /boot
limine-install --efi-directory=/boot <TARGET_DISK_DEV>
limine-mkconfig -o /boot/limine.conf
```

Note `limine-mkconfig` also handles generation of initrd, and copies kernel images to the correct place, thus there's no need to do so manually.

### Set Up Users

To log in the newly installed eweOS, a normal user must be added, or a password must be set for `root`

Please note `useradd` isn't available on eweOS, `adduser` provided by `busybox` could be used as alternative.

### Install Necessary Packages

Before rebooting into your new eweOS installation, some essential or helpful packages might be good to install,

#### Firmware Packages

Wireless NIC, graphics cards, and audio codec usually require firmware to function. They're included in Live environment, but not in the rootfs you've just installed. Here are some common cases,

- Intel wireless NIC: `linux-firmware-iwlwifi`
- Qualcomm/Atheros wireless NIC: `linux-firmware-atheros`
- MediaTek wireless NIC: `linux-firmware-mediatek`
- AMD Graphics Cards: `linux-firwware-amdgpu`
- Mellanox NIC: `linux-firmware-mellanox`

Please note that `linux-firwmare` doesn't pull in all firmware packages. It only contains firmware that is hard or isn't worth to categorize.

#### Network Management Tools

`wpa_supplicant` should be installed to connect to wireless network. You may want to install `networkmanager` to ease network configuration after the first boot, too.

#### sudo/doas

These are tools for running commands as other users, and in the mostly used case, as root. If you don't set `password` for root, one of them should be installed, or it's impossible to run privileged commands.
