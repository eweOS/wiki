---
title: makepkg Helpers
description: 
published: 1
date: 2023-11-23T14:28:12.803Z
tags: 
editor: markdown
dateCreated: 2023-11-23T14:27:37.678Z
---

# predefined functions

## `prepare` stage

### patch management

`_patch_ target_dir`:
- apply patches from source directory to specified directory
- number ordered patches are recommended

## `build` stage

### pick build artifacts

`_pick_ target pattern1 pattern2 ...`:
- pick a set of patterns of files to the specified name of directory inside the source directory

## `package` stage

### `dinit` files management

`_dinit_install_services_ file1 file2 ...`: (WIP)
- install dinit system service files

`_dinit_install_user_services_ file1 file2 ...`: (WIP)
- install dinit user service files

`_dinit_install_helpers_ file1 file2 ...`: (WIP)
- install dinit system helper files

`_dinit_install_user_helpers_ file1 file2 ...`: (WIP)
- install dinit user helper files

`_dinit_enable_services_ service1 service2 ...`: (WIP)
- enable (link to boot.d) dinit system service

`_dinit_enable_user_services_ service1 service2 ...`: (WIP)
- enable (link to boot.d) dinit user service

### `tmpfiles.d` / `sysusers.d` management

### license management

`_install_license_ file`: (WIP)
- install a license file as the name of current package

`_install_license_ file target_name` (WIP)
- install a license file as specified name inside the directory of the current package

# checkers

## directory checker