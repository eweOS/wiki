This will be the page of musl introduction and troubleshooting.

# Trouble Shooting
## undefined reference to {get,set,swap}context
Musl doesn't implement these functions because they are considered to be deprecated in POSIX standards. However this is still being used, for example, in `libxcrypt`.
To address this problem, install `libucontext` and add `-lucontext` to compile parameters.

## fatal: library not found: c
The linker tries to link to musl static libs but failed. You can install `musl-static`, but the better way is to figure out if linking against static libc can be avoided.

## fatal error: 'sys/{queue,cdefs,tree}.h' file not found
Install `bsd-compat-headers`. Remember also set sys-{queue,cdefs,tree}.h (the one that not found) as depends if you are making a package.

## fatal error: 'fts.h' file not found
Install `musl-fts`. Remember also set `musl-fts` as makedepends if you are making a package. You may also add `-lfts` to LDFLAGS if you see `undefined symbol: fts_{open,close,read}`

## fatal error: 'crypt.h' file not found
Install `libxcrypt`. Remember also set `libxcrypt` as makedepends.