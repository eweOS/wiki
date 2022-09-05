This will be the page of musl introduction and troubleshooting.

# Trouble Shooting
## undefined reference to {get,set,swap}context
Musl doesn't implement these functions because they are considered to be deprecated in POSIX standards. However this is still being used, for example, in `libxcrypt`.
To address this problem, install `libucontext` and add `-lucontext` to compile parameters.