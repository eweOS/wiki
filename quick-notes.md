# Quick Notes

## Packages

### busybox

- ~~remove `halt` `poweroff` `reboot` for `dinit`~~ (Finished)
- ~~remove `lspci` for `pciutils`~~ (Finished)
- ~~enable `ash` for initramfs~~ (Finished)

### mkinitramfs

- ~~remove `bash`~~ (Finished)
- ~~replace `bash` and `sh` with `ash`~~ (Finished)

### utmps

- A patch is introduced (`compat-path.patch`) to add additional defines to allow build of dinit. (Note)

## Architecture

Currently: x86

Roadmap: arm64 riscv64 (as Tier-1 support)

- `mold` have no riscv64 support yet.