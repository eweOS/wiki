# Quick Notes

## Packages

### busybox

- ~~remove `halt` `poweroff` `reboot` for `dinit`~~ (Finished)
- ~~remove `lspci` for `pciutils`~~ (Finished)
- ~~enable `ash` for initramfs~~ (Finished)

### mkinitramfs

- remove `bash`
- replace `bash` and `sh` with `ash`

## Architecture

Currently: x86

Roadmap: arm64 riscv64 (as Tier-1 support)

- `mold` have no riscv64 support yet.