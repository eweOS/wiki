# LLVM

## Special Sub-Packages

`llvm-libs`: `libcxx` `libcxxabi` `libunwind`
> These packages are installed in minimal system since most programs depend on them.

`llvm-lto`: `libLTO.so*`
> LTO lib. Required by linkers.

`clang`: `clang` `compiler-rt`
> `compiler-rt` is needed by clang.

`unknown`: `libLLVM*.a`
> llvm-static libs, used to bootstrap `rust`.

## Common Flags

- `CMAKE_BUILD_TYPE` : Release.
- `LLVM_ENABLE_PROJECTS` :
  - `lld` for `lld` package. (Default `ld` currently)
  - `clang` for `clang` package. (Default `cc`)
  - `compiler-rt` `libcxx` `libcxxabi` `libunwind` are integrated into `llvm-libs`.
    - `compiler-rt` & `libunwind` are included from `llvm-libgcc`, so remove them from list. (Currently disabled)
  - `libclc` `openmp` `lldb` are extra libs.
- `LLVM_DEFAULT_TARGET_TRIPLE` : `$CHOST`.
- `LLVM_HOST_TRIPLE` : `$CHOST`.
- `LLVM_ENABLE_PER_TARGET_RUNTIME_DIR` : OFF. We'll not seperate target dir by default.
- `LLVM_BUILD_LLVM_C_DYLIB` : ON. We'll build shared libs by default.
- `LLVM_LINK_LLVM_DYLIB` : ON. We'll also link shared libs.
- `LLVM_LIBGCC_EXPLICIT_OPT_IN` : ON. We'll use llvm-libgcc to improve compatibility.

## `llvm` Flags

- `LLVM_INSTALL_UTILS` : ON. We'll install llvm utils.
- `LLVM_ENABLE_LIBCXX` : ON. We'll use libc++.
- `DLLVM_ENABLE_RTTI` : ON. We'll support EH.
- `LLVM_ENABLE_FFI` : ON. We'll use `libffi`.
- `LLVM_ENABLE_LLD` : ON. We'll use `lld` to link LLVM.
- `LLVM_INSTALL_BINUTILS_SYMLINKS` : ON. We'll use llvm utils to replace GNU binutils.
- `LLVM_BUILD_LLVM_DYLIB` : ON. We'll build `libllvm` dynlib.
- `LLVM_INCLUDE_BENCHMARKS` : OFF. We'll temporary disable benchmark.
- `LLVM_TARGETS_TO_BUILD` : `X86;AArch64;RISCV`. Main supported targets.
- `LLVM_LINK_LLVM_DYLIB` : ON. Build tools using `libllvm`.
- `LLVM_BINUTILS_INCDIR` : `$srcdir/binutils-${_binutilsver}/include`. We'll use GNU binutils to generate libLLVMgold.so to provide lto support.

## `clang` Flags

- `CLANG_DEFAULT_CXX_STDLIB` : `libc++`. We use `libc++` for C++ lib.
- `CLANG_DEFAULT_RTLIB` : `compiler-rt`. We use `compiler-rt`.

## `libcxx/abi` Flags

- `LIBCXX_HAS_MUSL_LIBC` : ON. Use `musl`.
- `LIBCXX_USE_COMPILER_RT` : ON. 
- `LIBCXX_INCLUDE_TESTS` : OFF. Currently we don't need tests.
- `LIBCXX_INCLUDE_BENCHMARKS` : OFF. We'll temporary disable benchmark.
- `LIBCXXABI_USE_LLVM_UNWINDER` : ON. We use `libc++abi` for C++ ABI.
- `LIBCXX_USE_COMPILER_RT` : ON. We use `compiler-rt`.
- `LIBCXXABI_USE_COMPILER_RT` : ON. We use `compiler-rt`.

## `libunwind` Flags

- `LIBUNWIND_USE_COMPILER_RT` : ON. We use `compiler-rt`.
- `LIBUNWIND_INSTALL_HEADERS` : ON. We need libunwind headers to compile llvm.

## `compiler-rt` Flags

- `DCOMPILER_RT_BUILD_SANITIZERS` : OFF. Not supported for musl.
- `DCOMPILER_RT_BUILD_XRAY` : OFF. Not supported for musl.