# eweOS Installation Guide

> This is the **Official** installation guide.

## Image Types

- **Filesystem** images: Only base system with some extra tools, suitable to run in chroot or container environments.
- **Disk** images: Contain base system with linux kernel image and some tools used by generating bootable images. Suitable to run in QEMU via direct kernel boot.

> Currently disk images contain no initramfs since autobuild scripts are not fully functional.

