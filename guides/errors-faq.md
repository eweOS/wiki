# Errors FAQ

## `undefined reference to _Unwind_Resume`

- Add `LDFLAGS="-fuse-ld=lld -rtlib=compiler-rt -unwindlib=libunwind"`