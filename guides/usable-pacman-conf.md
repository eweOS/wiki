# Currently Usable pacman.conf

```
[options]
HoldPkg     = pacman musl
Architecture = auto
Color
CheckSpace
ParallelDownloads = 8

[core]
SigLevel = Never
Server = http://os-repo.ewe.moe/eweos/core/x86_64/

[boot]
SigLevel = Never
Server = http://os-repo.ewe.moe/eweos/boot/x86_64/

[kernel]
SigLevel = Never
Server = http://os-repo.ewe.moe/eweos/kernel/x86_64/

[extra]
SigLevel = Never
Server = http://os-repo.ewe.moe/eweos/extra/x86_64/

[desktop]
SigLevel = Never
Server = http://os-repo.ewe.moe/eweos/desktop/x86_64/
```