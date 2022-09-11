# Launch Prebuilt Image


```
#!/bin/bash

qemu-system-x86_64 \
	-smp 8 -m 4G -cpu host \
	-machine type=q35,accel=kvm \
        -kernel eweOS-rollingrelease.x86_64-1.0.0-5.19.3.kernel \
        -nographic \
        -append "console=ttyS0 root=/dev/sda rw" \
       	-hda eweOS-rollingrelease.x86_64-1.0.0 \
	-device virtio-net,netdev=ewe -netdev user,id=ewe \
	-device virtio-gpu,addr=3
```