# Create Non-bootable Disk Image

All-in-one script (from a installed Archlinux):

```
#!/bin/bash

dd if=/dev/zero of=testos.img bs=1M count=2048
sudo mkfs.ext4 ./testos.img
mkdir -p ./test-os
sudo mount ./testos.img ./test-os

sudo pacstrap -C ./pacman.conf ./test-os neofetch ca-certs base dinit vim linux mkinitramfs
echo "eweos-img" | sudo tee ./test-os/etc/hostname
sudo cp ./pacman.conf ./test-os/etc/pacman.conf

cat /etc/resolv.conf | sudo tee ./test-os/etc/resolv.conf
sudo arch-chroot ./test-os bash -c "mkinitramfs -o /boot && passwd"

cp ./test-os/boot/initrd.gz ./
cp ./test-os/usr/lib/modules/*/vmlinux ./

sudo umount ./test-os

qemu-system-x86_64 -m 1G -hda testos.img -kernel vmlinux -initrd initrd.gz -nographic -append "console=ttyS0 root=/dev/sda" -device virtio-net,netdev=ewe -netdev user,id=ewe
```

A copy of usable `pacman.conf` can be found at [here](https://os-wiki.ewe.moe/guides/usable-pacman-conf).