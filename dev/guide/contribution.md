---
title: Contributing Guide
description: 
published: 1
date: 2023-10-19T07:21:57.769Z
tags: 
editor: markdown
dateCreated: 2023-10-19T06:47:52.080Z
---

Before your contribution, here's some rules that needs to adhere.

## Commit and Pull Request Format

### [eweOS/packages](https://github.com/eweOS/packages)

```
[<pkgname>] <pkgver>: <brief description>

<optional long description>
```

Brief description should start in lowercase (if applicable).

For example, when upgrading `dummypkg`:

```
[dummypkg] 0.1.0-2: remove some patches

Upstream merged and fixed: https://github.com/...
```

Adding a new package:

```
[newpkg] 1.0.0-1: initial packaging
```