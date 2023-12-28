---
title: eweOS Wiki
description: Too Young - Too Simple - Sometimes Naive
published: 1
date: 2023-12-28T09:09:04.523Z
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

## User Guides

> **WIP**: Currently, eweOS is too early to be used in production and primary devices. Please wait patiently for our latest news.

- :computer: [Boot Disk Image](/guides/boot-diskimage) - Tutorial to launch prebuilt disk images via QEMU
- :package: [Software & Configuration](/guides/softwares) - List of supported softwares and tutorials to configure them
- :raising_hand: [FAQ](/guides/faq) - Some frequently asked questions
- :fire: [Report bugs and give feedbacks](https://github.com/eweOS/bugs/issues) - Use GitHub issues to post your bug reports

## Developer Resources

### Guides

- **Packaging**
  - :package: [Packaging Guidelines](/dev/guide/packaging) - Brief introduction for packaging in eweOS
  - :question: [Troubleshooting](/dev/guide/troubleshooting) - Common problems and solutions

- **System Images**
	- :cd: [Build EFI Live USB Image](/dev/guide/build-efi-liveusb-img) - Tutorial to build EFI bootable Live USB Disk Image from prebuilt `squashfs` and `efistub`

- **Contribution**
	- :book: [Contributing Guide](/dev/guide/contribution) - Rules and formats for every contribution

### Topics

- **Toolchain & Runtime**
[musl](/dev/topic/toolchain/musl) • [LLVM/Clang](/dev/topic/toolchain/llvm) • [Lua](/dev/topic/toolchain/lua) • [Java](/dev/topic/toolchain/java) • [Python](/dev/topic/toolchain/python) • [Rust](/dev/topic/toolchain/rust) • [SPIR-V](/dev/topic/toolchain/spirv)

- **Desktop**
[Desktop Environment](/dev/topic/desktop/desktop-env) • [Multimedia](/dev/topic/desktop/multimedia)

- **Graphics**
[QT](/dev/topic/graphics/qt) • [GTK](/dev/topic/graphics/gtk)

- **Kernel & Driver**
*WIP*

- **Architectures**
Tier 0 support (Full Main Repo, Testing Repo, Workflow): x86_64
Tier 1 support (90% Main Repo, Testing Repo, Workflow): [ARM (aarch64)](/dev/topic/arch/arm)
Tier 1.5 support (Main Repo, Testing Repo): [RISC-V (riscv64)](/dev/topic/arch/riscv)
Community support (eweOS-ports): -

- **Network/Storage**
*WIP*

- **System Utilities**
[Bootloader](/dev/topic/sysutils/bootloader) • [Shell](/dev/topic/sysutils/shell) • [Core Utilities](/dev/topic/sysutils/coreutils) • [dinit](/dev/topic/sysutils/dinit)

- **Packaging**
[makepkg Helpers](/dev/topic/packaging/makepkg-helpers) • [PKGBUILD templates](/dev/topic/packaging/pkgbuild-templates)

- **Infrastructure**
[Automatic Workflow](/dev/topic/infra/auto-workflow) • [Repositories](/dev/topic/infra/repos)

- **Security**
*WIP*

- **Packages Special**
*WIP*

### Development Quick Notes

- :clipboard: [Quick Notes](/dev/quick-notes) - Rapidly updated notepad for project management of contributors
- :clipboard: [TODO](/dev/todo) - To-do list
- :repeat: [Software Replacements](/dev/replacements) - Lists and status of alternatives we used in eweOS and a list of unsupported and dropped softwares

## Legal & Contracts

- [Code of Conduct]()
*WIP*

## See Also

- :package: [Subprojects](/see-also/subprojects) - Projects developed and used by eweOS
- :busts_in_silhouette: [Similar projects](/see-also/similar-projects) - Other similar distros and projects
- :information_source: [Github Repos](/see-also/github-repos) - Information about repositories at GitHub
