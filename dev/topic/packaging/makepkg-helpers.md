---
title: makepkg Helpers
description: 
published: 1
date: 2023-11-24T05:55:53.138Z
tags: 
editor: markdown
dateCreated: 2023-11-23T14:27:37.678Z
---

makepkg helpers are groups of scripts used for stages in packaging. These scripts are located at `/usr/share/makepkg`.

# predefined functions

## `prepare` stage

### patch management

`_patch_ target_dir`:
- apply patches from source directory to specified directory
- number ordered patches are recommended

## `build` stage

### pick build artifacts

`_pick_ target pattern1 pattern2 ...`:
- pick a set of patterns of files to the specified name of directory inside `$srcdir/pkgs/$target`
- example: 
	- `_pick_ amdgpu usr/lib/firmware/amdgpu` will extract all files in `usr/lib/firmware/amdgpu` into `$srcdir/pkgs/amdgpu`

## `package` stage

### `dinit` files management

`_dinit_install_services_ file1 file2 ...`: (WIP)
- install dinit system service files
- example:
  - `_dinit_install_services_ $srcdir/dbus.service` will install `dbus.service` into dinit system service directory as the name of `dbus`.

`_dinit_install_user_services_ file1 file2 ...`: (WIP)
- install dinit user service files
- example:
  - `_dinit_install_user_services_ $srcdir/dbus.user.service` will install `dbus.service` into dinit user service directory as the name of `dbus`.

`_dinit_install_helpers_ file1 file2 ...`: (WIP)
- install dinit system helper files
- example:
  - `_dinit_install_helpers_ $srcdir/dbus-system-session` will install `dbus-system-session` into dinit system service helper directory.

`_dinit_install_user_helpers_ file1 file2 ...`: (WIP)
- install dinit user helper files
- example:
  - `_dinit_install_user_helpers_ $srcdir/dbus-user-session` will install `dbus-user-session` into dinit system service helper directory.

`_dinit_enable_services_ service1 service2 ...`: (WIP)
- enable (link to boot.d) dinit system service
- example:
  - `_dinit_enable_services_ ntpd` will enable spefcified system services by create symlinks.

`_dinit_enable_user_services_ service1 service2 ...`: (WIP)
- enable (link to boot.d) dinit user service
- example:
  - `_dinit_enable_user_services_ dbus` will enable spefcified user services by create symlinks.

### `tmpfiles.d` / `sysusers.d` management

### license management

`_install_license_ file`: (WIP)
- install a license file as the name of current package
- example:
  - `_install_license_ $srcdir/COPYING` will install `COPYING` into license directory as the name of current package

`_install_license_ file target_name` (WIP)
- install a license file as specified name inside the directory of the current package
- example:
  - `_install_license_ $srcdir/COPYING COPYING` will install `COPYING` into license directory, inside the directory of the current package

# checkers

## directory checker

in `lint` stage, if `pkgdir` contains these directories, directory checker would throw an error:

- `/lib`
- `/lib64`
- `/usr/lib64`
- `/bin`
- `/sbin`
- `/var/run`