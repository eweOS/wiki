# Setting up rootfs
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

# Setting up inside qemu
Firstly inside the chroot container you've created, install several needed packages:
```
# pacman -Sy linux linux-headers dinit mkinitramfs
```
Make a initrd,
```
# mkinitramfs
```
Then copy generated /tmp/initrd.gz out of eweos chroot(without exiting it!). Also copy /usr/lib/modules/(The version of kernel)/vmlinux outside. If you already have qemu-system installed, issue (save as a shell script for convenience)
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