```
#!/bin/bash

export DESTDIR="/root/dst"

cd $DESTDIR && find . -name *.a -delete

function fetchpkg() {
	PKGBASE=$1 && shift
	echo "Installing package $PKGBASE..."
	PKGDEST="/root/pkgs/$PKGBASE"
	mkdir -p $PKGDEST
	for FILEPATH in $@; do
		echo "Installing path $FILEPATH..."
		(cd $DESTDIR && find $FILEPATH | cpio -pdvmu "$PKGDEST")
		(cd $DESTDIR && find $FILEPATH -delete)
	done
}

FLIST=(
	"usr/bin/*clang*"
	"usr/bin/c-index-test"
	"usr/bin/cc"
	"usr/bin/c++"
	"usr/lib/cmake/clang"
	"usr/share/clang"
	"usr/include/clang-c"
	"usr/include/clang"
	"usr/lib/libclang*.so"
	"usr/bin/analyze-build"
	"usr/bin/intercept-build"
	"usr/bin/scan-*"
	"usr/lib/libear"
	"usr/lib/libscanbuild"
	"usr/libexec/analyze-*"
	"usr/libexec/*analyzer"
	"usr/libexec/intercept-*"
	"usr/share/scan-*"
	"usr/share/man/man1/scan-build.1"
	"usr/lib/libclang.so.*"
	"usr/lib/libclang-cpp.so.*"
)
fetchpkg "clang" "${FLIST[@]}"

FLIST=(
	"usr/lib/clang"
)
fetchpkg "compiler-rt" "${FLIST[@]}"

FLIST=(
	"usr/bin/*lldb*"
	"usr/lib/liblldb*.so.*"
	"usr/include/lldb"
	"usr/lib/liblldb*.so"
)
fetchpkg "lldb" "${FLIST[@]}"

FLIST=(
	"usr/include/ompt-multiplex.h"
	"usr/lib/cmake/openmp"
	"usr/lib/libomptarget-*.bc"
	"usr/lib/libomptarget*.so*"
	"usr/lib/libarcher*.so"
	"usr/lib/libomp*.so"
	"usr/lib/libgomp.so"
	"usr/lib/libiomp5.so"
)
fetchpkg "openmp" "${FLIST[@]}"

FLIST=(
	"usr/bin/ld"
	"usr/bin/lld*"
	"usr/bin/wasm-ld"
	"usr/bin/ld.lld*"
	"usr/bin/ld64.lld*"
	"usr/include/lld"
	"usr/lib/cmake/lld"
)
fetchpkg "lld" "${FLIST[@]}"

FLIST=(
	"usr/lib/libLTO.so*"
	"usr/lib/libRemarks.so*"
	"usr/lib/libc++.so.*"
	"usr/lib/libc++abi.so.*"
	"usr/lib/libc++.so"
	"usr/lib/libc++abi.so"
	"usr/include/*cxxabi*"
	"usr/include/c++"
	"usr/lib/libunwind.so.*"
	"usr/lib/libunwind.so"
	"usr/include/*unwind*"
)
fetchpkg "llvm-libs" "${FLIST[@]}"
```