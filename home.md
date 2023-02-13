---
title: eweOS Wiki
description: Too Young - Too Simple - Sometimes Naive
published: 1
date: 2023-02-13T14:29:15.397Z
tags: 
editor: markdown
dateCreated: 2023-02-13T14:12:29.050Z
---

# **Welcome to eweOS wiki!**

<div style="display: inline-block;">
<img src="/logo.png" alt="eweOS Logo" width="100" style="float: left; margin-right: 10px;"/>
eweOS is an musl-based, lightweight, general-purpose Linux distribution, which adopts musl libc and busybox to the latest versions of software with a rolling-release model.
</div>

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

- [musl](/dev/topic/toolchain/musl)
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
- [:repeat: Software Replacements *Lists and status of alternatives we used in eweOS and a list of unsupported softwares*](/dev/replacements)
{.links-list}
