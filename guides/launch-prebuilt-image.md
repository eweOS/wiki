# Launch Prebuilt Image

You need to download prebuild at [here](https://os-repo.ewe.moe/eweos-images/), extract kernel and disk image.

```
#!/bin/bash

qemu-system-x86_64 \
	-smp 8 -m 4G -cpu host \
	-machine type=q35,accel=kvm \
        -kernel eweOS-rollingrelease.x86_64-1.0.0-6.0.kernel \
        -nographic \
        -append "console=ttyS0 root=/dev/sda rw" \
       	-hda eweOS-rollingrelease.x86_64-1.0.0 \
	-device virtio-net,netdev=ewe -netdev user,id=ewe \
	-device virtio-gpu,addr=3
```

Login with username `root` and password `ewe`.

## NOTICE

It is needed to renew your kernel outside the image after a kernel update. The updated kernel is in ``/usr/lib/modules/VERSION/vmlinuz``. One possible way is to attach the image to a loop device, mount the loop device,
copy the new kernel out then update your bootstrap script.