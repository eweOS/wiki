---
title: eweOS Wiki
description: Too Young - Too Simple - Sometimes Naive
published: 1
date: 2025-09-30T17:05:32.232Z
tags: 
editor: markdown
dateCreated: 2023-02-13T14:12:29.050Z
---

<div style="display: inline-block; padding-top: 20px;">
<img src="/logo.png" alt="eweOS Logo" width="100" style="float: left; margin-right: 10px;"/>
eweOS is an musl-based, lightweight, general-purpose Linux distribution, which adopts musl libc and busybox to the latest versions of software with a rolling-release model. Also, it's fun!
</div>

## Useful Links

- :house: [Home Page](https://os.ewe.moe) - Home page of eweOS project
- :notebook_with_decorative_cover: [Wiki](https://os-wiki.ewe.moe) - This website, some tutorials and info about eweOS project
- :package: [Repo](https://os-repo.ewe.moe) - Download eweOS packages, system images and resources for developers
- :hammer: [Build System](https://os-build.ewe.moe) - An automatic and open platform for eweOS developers to build packages
- :computer: [Test Server](https://os-test.ewe.moe) - Unstable eweOS web server for showcasing
- :package: [Installation Guide](https://os-wiki.ewe.moe/en/guides/installation-guide) – Step-by-step guide to install eweOS on your system.


## User Guides

> **WIP**: Currently, eweOS is too early to be used in production and primary devices. Please wait patiently for our latest news.

- :computer: [Boot ISO Image from QEMU](/guides/qemu-boot-isoimage) - Tutorial to launch prebuilt iso images via QEMU
- :package: [Software & Configuration](/guides/softwares) - List of supported softwares and tutorials to configure them
- :raising_hand: [FAQ](/guides/faq) - Some frequently asked questions
- :fire: [Report bugs and give feedbacks](https://github.com/eweOS/bugs/issues) - Use GitHub issues to post your bug reports

## Developer Resources

### Guides

- **Packaging**
  - :package: [Packaging Guidelines](/dev/guide/packaging) - Brief introduction for packaging in eweOS
  - :question: [Troubleshooting](/dev/guide/troubleshooting) - Common problems and solutions

- **System Images**
	- :cd: [Build eweOS Image](/dev/guide/build-image) - Tutorial to build bootable Live Image or tarball from eweOS `iso` scripts

- **Contribution**
	- :book: [Contributing Guide](/dev/guide/contribution) - Rules and formats for every contribution

### Topics

- **Toolchain & Runtime**
[musl](/dev/topic/toolchain/musl) • [LLVM/Clang](/dev/topic/toolchain/llvm) • [Lua](/dev/topic/toolchain/lua) • [Java](/dev/topic/toolchain/java) • [Python](/dev/topic/toolchain/python) • [Rust](/dev/topic/toolchain/rust) • [Vulkan/SPIR-V](/dev/topic/toolchain/vulkan-spirv)

- **Desktop**
[Desktop Environment](/dev/topic/desktop/desktop-env)
[Multimedia](/dev/topic/desktop/multimedia)
[Fonts](/dev/topic/desktop/fonts)
[wlroots](/dev/topic/desktop/wlroots)

- **Graphics**
[QT](/dev/topic/graphics/qt) • [GTK](/dev/topic/graphics/gtk)

- **Kernel & Driver**
[Kernel](/dev/topic/kernel)

- **Architectures**
Tier 1 support (Main Repo, Testing Repo, Workflow): x86_64, [ARM (aarch64)](/dev/topic/arch/arm)
Tier 1 support (Main Repo, Testing Repo): [RISC-V (riscv64)](/dev/topic/arch/riscv) [LoongArch64 (loongarch64)](/dev/topic/arch/loongarch)
Community support (eweOS ports):

- **Network**
[ifupdown-ng](/dev/topic/network/ifupdown-ng) [NetworkManager](/dev/topic/network/NetworkManager)

- **Storage**
*WIP*

- **System Utilities**
[Bootloader](/dev/topic/sysutils/bootloader) • [Shell](/dev/topic/sysutils/shell) • [Core Utilities](/dev/topic/sysutils/coreutils) • [dinit](/dev/topic/sysutils/dinit) • [catnest (sysusers)](/dev/topic/sysutils/catnest)

- **Packaging**
[makepkg Helpers](/dev/topic/packaging/makepkg-helpers) • [PKGBUILD templates](/dev/topic/packaging/pkgbuild-templates) • [Meta Packages](/dev/topic/packaging/metapackages) • [Guideline for Writing pkgdesc](/dev/topic/packaging/pkgdesc-guideline)

- **Infrastructure**
[Automatic Workflow](/dev/topic/infra/auto-workflow) • [Repositories](/dev/topic/infra/repos)

- **Security**
*WIP*

- **Packages Special**
*WIP*

- **Compatibility**
[musl vs glibc](/dev/topic/compat/musl-glibc) • [clang vs gcc](/dev/topic/compat/clang-gcc) • [dinit vs systemd](/dev/topic/compat/dinit-systemd) • [libudev-zero vs systemd-udev](/dev/topic/compat/libudevzero-systemdudev)

### Development Notes

- :clipboard: [TODO](/dev/todo) - To-do list
- :repeat: [Software Replacements](/dev/replacements) - Lists and status of alternatives we used in eweOS and a list of unsupported and dropped softwares

## Community

- [Community Membership](/community/membership)

<!--
## Activities

- [Google Summer of Code 2025](/activities/gsoc)

-->

## See Also

- :package: [Subprojects](/see-also/subprojects) - Projects developed and used by eweOS
- :busts_in_silhouette: [Similar projects](/see-also/similar-projects) - Other similar distros and projects
- :information_source: [Github Repos](/see-also/github-repos) - Information about repositories at GitHub
