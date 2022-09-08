# LLVM

## Common Flags

- `CMAKE_BUILD_TYPE` : Release.

## `libcxx/abi` Flags

- `LIBCXX_HAS_MUSL_LIBC` : ON. Use `musl`.
- `LIBCXX_USE_COMPILER_RT` : ON. 
- `LIBCXX_INCLUDE_TESTS` : OFF. Currently we don't need tests.
- `LIBCXXABI_USE_LLVM_UNWINDER` : ON. We use `libc++abi` for C++ ABI.
- `LIBCXX_USE_COMPILER_RT` : ON. We use `compiler-rt`.
- `LIBCXXABI_USE_COMPILER_RT` : ON. We use `compiler-rt`.
- 