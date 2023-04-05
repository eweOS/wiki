---
title: Lua
description: Information about Lua toolchain
published: 1
date: 2023-04-05T04:51:15.362Z
tags: 
editor: markdown
dateCreated: 2023-04-05T04:51:15.362Z
---

# Lua

The standalone Lua interpreter and Lua libraries are included in `lua5x` packages.

| Version  | 5.0 | 5.1 | 5.2 | 5.3 | 5.4 |
|----------|-----|-----|------------------
| Supported?| X  | \*  | X   | X   | \*  |

- `V`: Lua with luarocks
- `*`: Lua only
- `x`: Not supported

## Lua Libraries and Headers

In order to keep different Lua versions coexisting, the following rules are used.

- Shared libraries are kept in `/usr/lib/lua5.x/`, with a symbol link named `liblua.so` referring to it.
- To make it possbile for dynamic linker to find the shared libraries, symbol links `/usr/lib/liblua-5.x.so` refers to the corresponding library.
- Static libraries are located at the same directory as shared ones.
- C headers are located at `/usr/include/lua5.x/`
- pkg-config configuration (`*.pc`) is included in the package and the Lua packages are named like
`lua5.x` and `lua5.x-c++`. The later is a symbol link to the former.

## Lua Modules

Lua modules store at `/usr/share/lua` and `/usr/lib/lua`. The former is for Lua-only modules, the later is for C-only/combined modules.

Modules are splited by version. There is a special `common` directory, in which modules could be accessed by all versions Lua interpreter.

## luarocks

TODO