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