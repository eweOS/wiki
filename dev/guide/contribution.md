---
title: Contributing Guide
description: 
published: 1
date: 2024-04-29T09:33:28.384Z
tags: 
editor: markdown
dateCreated: 2023-10-19T06:47:52.080Z
---

## Where to Contribute

Most of eweOS development takes place at [eweOS package repository](https://github.com/eweOS/packages). To modify or create a package, you should fork the repository first.

eweOS package repository contains multiple branches, with each PKGBUILD file assigned to one.

## Upgrade/Modify an Existing Package

Simply create a pull request to eweOS package repository.

For upgrading, the commit message should be like:

```
[<pkgname>] <pkgver>-<pkgrel>: new upstream version

<optional long description>
```

You could refer to this [pull request](https://github.com/eweOS/packages/pull/169).

## Create New Packages

To create new packages, you should create an issue in eweOS package repository with title like:

```
[<pkgname>] <pkgver>: new package
```

Add link to your fork of eweOS package repository and specify a branch in the issue. The maintainer will check it (and maybe require changes).

Your branch should contains only one commit with message like

```
[<newpkg>] <pkgver>-1: init package
```

## General Commit Format

```
[<pkgname>] <pkgver>-<pkgrel>: <brief description>

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
[newpkg] 1.0.0-1: init package
```