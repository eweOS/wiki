---
title: Build eweOS Image
description: Tutorial to build bootable Live Image or tarball from eweOS iso scripts
published: 1
date: 2024-04-29T09:27:19.463Z
tags: 
editor: markdown
dateCreated: 2024-04-29T09:24:57.488Z
---

# Repository

eweOS uses [iso](https://github.com/eweOS/iso) scripts to create bootable images and tarballs.

# Usage

1. clone iso repository
```
git clone https://github.com/eweOS/iso
```

2. install dependency:

- `squashfs-tools`: for squashfs creation
- `arch-install-scripts`: for `pacstrap` and `arch-chroot`
- `libisoburn`: for `xorriso`
- `wget`: for file downloading

3. usage:

```
./gen.sh {profile} [arch]
```

4. find and use artifacts in `./results/` directory

# Customize

See [README.md](https://github.com/eweOS/iso/blob/master/README.md)

And contribution is welcomed!