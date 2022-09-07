# Currently Usable pacman.conf

```
[options]
HoldPkg     = pacman musl
Architecture = auto
Color
CheckSpace
ParallelDownloads = 8

[minimal]
SigLevel = Never
Server = http://os-repo.ewe.moe/eweos/minimal/x86_64/

[boot]
SigLevel = Never
Server = http://os-repo.ewe.moe/eweos/boot/x86_64/

[develop]
SigLevel = Never
Server = http://os-repo.ewe.moe/eweos/develop/x86_64/

[kernel]
SigLevel = Never
Server = http://os-repo.ewe.moe/eweos/kernel/x86_64/

[misc]
SigLevel = Never
Server = http://os-repo.ewe.moe/eweos/misc/x86_64/

[misclibs]
SigLevel = Never
Server = http://os-repo.ewe.moe/eweos/misclibs/x86_64/

[network]
SigLevel = Never
Server = http://os-repo.ewe.moe/eweos/network/x86_64/

[desktop]
SigLevel = Never
Server = http://os-repo.ewe.moe/eweos/desktop/x86_64/
```