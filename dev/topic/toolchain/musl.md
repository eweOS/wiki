---
title: musl libc
description: 
published: 1
date: 2023-05-24T13:37:36.435Z
tags: 
editor: markdown
dateCreated: 2023-05-24T08:55:41.848Z
---

# Related Packages

# Troubleshooting

## `no member named '{syscall_name}64'` || `incomplete type '{syscall_name}64'`

From 1.2.4, musl deprecates all LFS64 interfaces.

Solution: Add `D_LARGEFILE64_SOURCE` to `CFLAGS`/`CXXFLAGS` (will also be removed in a future version)

Here is a list of observed and fixed package for this issue, issues/PRs may be submitted to upstream:

- libpciaccess (fixed)
- libbsd (fixed)
- llvm
- efivar (fixed)
- btop
- acl
- nginx
- perl-module-build-tiny