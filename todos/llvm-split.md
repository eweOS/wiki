# TODO: Split LLVM Packages

Work Project: [eweOS:LLVM](https://os-build.ewe.moe/project/show/eweOS:LLVM)

## Packages

### Package `llvm` and `llvm-libs`

- llvm
- libcxx (libc++)
- libcxxabi (libc++abi)
- libunwind
(`libcxx` and `libcxxabi` can not be built without a mono repo)

### Other packages

- clang (as Default CC)
- lld (will be replaced with mold)
- compiler-rt

## Packages Standalone

- libclc (eweOS:Misclibs)

## Packages (Currently not used)

- lldb
- openmp
- lldb
- (Others)
