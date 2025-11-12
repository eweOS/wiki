---
title: Installation Guide
description: Installation Guide for EweOS using Jade
published: 1
date: 2025-10-01T11:36:08.307Z
tags: 
editor: markdown
dateCreated: 2025-09-30T16:21:19.491Z
---

# eweOS Installation Guide

This guide shows how to install eweOS using **Jade** only.  
No manual partitioning required. Works on both **UEFI** and **BIOS** systems.  

**NOTE: This is not (yet) functioning and is WIP!**

For more details see the [Jade documentation](https://github.com/eweOS/jade/blob/main/README.md).

---

## 1. Boot into Live System
- Write the eweOS (base) ISO to a USB stick.  
- Boot from it (choose "Live" in the menu).  
- You’ll be in a **terminal environment**.

---

## 2. Find Your Disk
List all drives:

```
lsblk
```

Example:

```
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda      8:0    0  120G  0 disk 
├─sda1   8:1    0  512M  0 part
└─sda2   8:2    0 119.5G 0 part
sdb      8:16   1   16G  0 disk /run/media/liveusb
```

👉 In this example, `/dev/sda` is the main hard drive.  
⚠️ Do **not** use your USB stick (e.g. `/dev/sdb`).

---

## 3. Partition Automatically

For **UEFI systems** (modern PCs):

```
jade partition auto /dev/sda --efi
```

For **BIOS/Legacy systems**:

```
jade partition auto /dev/sda
```

*(Replace `/dev/sda` with your actual disk.)*  
This will erase the disk and create partitions automatically.

---

## 4. Install Base System

```
jade install-base --kernel default
```

---

## 5. Install Bootloader

For **UEFI**:

```
jade bootloader limine-efi
```

For **BIOS/Legacy**:

```
jade bootloader limine-legacy /dev/sda
```

---

## 6. Generate fstab

```
jade genfstab
```

---

## 7. Configure Locale, Keyboard, Timezone

Example: English (US), Europe/Berlin timezone:

```
jade locale us Europe/Berlin en_US.UTF-8 UTF-8
```

---

## 8. Configure Networking

Set your hostname (example: `my-pc`):

```
jade networking my-pc
```

---

## 9. Create Users

Example user `alice` with root access:

```
jade users new-user alice mypassword bash --hasroot
jade users root-password rootpass
```

---

## 10. (Optional) Install a Desktop

Example: Hyprland:

```
jade desktops hyprland
```

---

## 11. Reboot

When finished:

```
reboot
```

You should now boot into eweOS!

---

## Notes
- All above command should run with superuser privilege.  
- Always run `lsblk` first to confirm the correct disk.  
- `jade partition auto` will **wipe the disk completely**.  
- Use the correct bootloader command depending on UEFI or BIOS mode.  
