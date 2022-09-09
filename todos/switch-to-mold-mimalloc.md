# Switch to mold and mimalloc

- ~~Step 1: Build `llvm-full` toolchain with `mold` and `mimalloc`.~~ (Finished)
- ~~Step 2: Build all packages with `mold` and `mimalloc`.~~ (Finished)
- ~~Step 3: Remove `lld->ld` symlink and replace it with `mold` in `base-devel`, add `mimalloc` to `base-devel`.~~ (Finished)

## LTO

We use `llvm` tools instead of `binutils`, so `gold` can not be built. Then `LLVMgold.so` can not be generated.

`mold` use `LLVMgold.so` for LTO, which is not possible currently.

Temporary solution: disable LTO for all packages, or use lld instead (also no LTO).