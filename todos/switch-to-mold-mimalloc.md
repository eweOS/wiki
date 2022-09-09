# Switch to mold and mimalloc

- Step 1: Build `llvm-full` toolchain with `mold` and `mimalloc`.
- Step 2: Build all packages with `mold` and `mimalloc`.
- Step 3: Remove `lld->ld` symlink and replace it with `mold` in `base-devel`, add `mimalloc` to `base-devel`.