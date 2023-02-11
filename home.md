---
title: Homepage
description: Home
published: 1
date: 2023-02-11T16:11:10.254Z
tags: 
editor: markdown
dateCreated: 2023-02-11T15:16:48.718Z
---

# **Welcome to eweOS wiki!**

eweOS is an musl-based, lightweight, general-purpose Linux distribution, which adopts musl libc and busybox to the latest versions of software with a rolling-release model.

> **Notice**: Wiki restructing is in progress, some pages may not working or missing.

## Why eweOS

It's fun.

## Useful Links

- [:house: HomePage *Homepage of eweOS project*](https://os.ewe.moe)
- [:notebook_with_decorative_cover: Wiki *This website, some tutorials and info about eweOS project*](https://os-wiki.ewe.moe)
- [:package: Repo *Download eweOS packages, system images and resources for developers*](https://os-repo.ewe.moe)
- [:hammer: BuildSystem *An automatic and open platform for eweOS developers to build packages*](https://os-build.ewe.moe)
- [:computer: TestServer *Unstable eweOS web server to previewing*](https://os-test.ewe.moe)
{.links-list}

## User Guides

> **WIP**: Currently, eweOS is too early to be used in production and primary devices. Please wait patiently for our latest news, or, why not becoming a developer of eweOS?

## Developer Resources

### Developer Guides {.tabset}

#### Packaging

- [:package: Packaging Guidelines *A brief introduction for packaging in eweOS*](/dev/guide/packaging)
{.links-list}

#### System Images

> Currently there is no officially built bootable disk image.
{.is-info}

- [:computer: Boot KIS Image *Tutorial to launch KIS(Kernel Initrd Sysroot) images via QEMU*](/dev/guide/launch-kis)
- [:cd: Build EFI Disk Image *Tutorial to build bootable EFI Disk Image*](/dev/guide/build-efi-disk-img)
{.links-list}

#### Discuss & Feedback

- [:fire: Report bugs and give feedbacks *Use GitHub issues to post your bug reports*](https://github.com/eweOS/bugs/issues)
{.links-list}

### Dev Topics {.tabset}

#### Toolchain/Runtime

- [LLVM/Clang](/dev/topic/toolchain/llvm)
- [Java](/dev/topic/toolchain/java)
- [Python](/dev/topic/toolchain/python)
- [Rust](/dev/topic/toolchain/rust)

#### Desktop

- [Desktop Environment](/dev/topic/desktop/desktop-env)
- [Multimedia](/dev/topic/desktop/multimedia)

#### Kernel/Driver

#### Architectures

Tier 0 support:
- x86_64

Tier 1 support:
- [ARM (aarch64)](/dev/topic/arch/arm)
- [RISC-V (riscv64)](/dev/topic/arch/riscv)

#### Network/Storage

#### System Utils

#### Infrastructure

- [Build System](/dev/topic/infra/build-system)

#### Packages Special

### Dev TODOs

- [Version Bumper](/dev/todo/version-bumper)
- [Switch to mold and mimalloc](/dev/todo/switch-to-mold-mimalloc)
- [Replace busybox](/dev/todo/replace-busybox)
- [(Programming) Language support](/dev/todo/pl-support)

### Dev Quick Notes

- [:clipboard: Quick Notes *Quick Notes is a rapidly updated notepad for project management of contributors*](/dev/quick-notes)
{.links-list}
