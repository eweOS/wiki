# Create Bootable Image

Currently eweOS have no bootloader built from source code. A choice is `clover-efi` from `eweOS:Boot`, which is a package built from binaries. 

`syslinux` and `grub` can not be built currently since `gcc` and/or `binutils` are required.

It's not sure ISO file can be built. But for disk images, here is a simple procedure:

- Create a disk using `dd` command: `dd if=/dev/zero of=eweos.img bs=1M count=2048`
- Create a GPT partition table, create and format EFI/rootfs partitions.
- Mount two partitions as `/` and `/boot`.
- Using `pacstrap` from `archlinux`, with customized `pacman.conf`, install `base` and other tools: `pacstrap -C ./pacman.conf ./mnt base ...`
- Chroot and configure `clover-efi`, a sample config is placed at `/usr/share/clover-efi/config.plist.sample`.
- Run `mkinitramfs -o /boot` to generate `initrd.gz` at `/boot` and place kernel image from `/usr/lib/modules/<linux_ver>/vmlinux` to `/boot`. 
- Use it.