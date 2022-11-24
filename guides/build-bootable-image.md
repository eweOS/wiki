```
#!/bin/bash

echo "Cleaning env..."

sudo umount ./test-os/boot || true
sudo umount ./test-os/ || true
./clean.sh

echo "Creating disk..."

dd if=/dev/zero of=testos.img bs=1M count=6000
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
) | fdisk ./testos.img

echo "Setting up loop device..."

LODEV=`sudo losetup -P -f --show ./testos.img`
SYSDEV=${LODEV}p2
BOOTDEV=${LODEV}p1

echo "Formatting loop device..."

sudo mkfs.ext4 ${SYSDEV}
sudo e2label ${SYSDEV} EWE_ROOT
sudo mkfs.fat -F 32 ${BOOTDEV}

echo "Making mountpoint..."

mkdir -p ./test-os
sudo mount ${SYSDEV} ./test-os
sudo mkdir -p ./test-os/boot
sudo mount ${BOOTDEV} ./test-os/boot

echo "Installing packages..."

sudo pacstrap -C ./pacman.internal.conf ./test-os neofetch ca-certs base dinit linux mkinitramfs vim base-devel efistub

echo "Setting up system..."

echo "eweos-img" | sudo tee ./test-os/etc/hostname
sudo cp ./pacman.conf ./test-os/etc/pacman.conf
cat /etc/resolv.conf | grep nameserver | sudo tee ./test-os/etc/resolv.conf
echo "virtio_net" | sudo tee ./test-os/etc/modules
sudo ln -s ../modules ./test-os/etc/dinit.d/boot.d
sudo ln -s ../udhcpc ./test-os/etc/dinit.d/boot.d

echo "" > initsettings.sh
cat <<EOF >>initsettings.sh
#!/bin/bash
genefistub

echo "Changing password to root:ewe ..."
echo "root:ewe" | chpasswd
rm ./initsettings.sh
EOF

sudo cp ./initsettings.sh ./test-os/root
rm ./initsettings.sh

sudo arch-chroot ./test-os bash -c "cd && chmod +x initsettings.sh && ./initsettings.sh"

sleep 2

echo "Umounting loop devices..."

sudo umount ./test-os/boot
sudo umount ./test-os
sudo losetup -d $LODEV
```