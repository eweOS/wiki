# Currently Usable pacman.conf

```
[options]
HoldPkg     = pacman glibc
Architecture = auto
Color
CheckSpace
ParallelDownloads = 8

[core]
SigLevel = Never
Server = http://repo.nia.dn42/eweos/core/x86_64/

[boot]
SigLevel = Never
Server = http://repo.nia.dn42/eweos/boot/x86_64/

[kernel]
SigLevel = Never
Server = http://repo.nia.dn42/eweos/kernel/x86_64/

[extra]
SigLevel = Never
Server = http://repo.nia.dn42/eweos/extra/x86_64/
```