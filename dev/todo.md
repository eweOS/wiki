---
title: TODO
description: A list of TODOs
published: 1
date: 2025-02-11T14:47:42.829Z
tags: 
editor: markdown
dateCreated: 2023-02-25T04:24:22.548Z
---

> **This is an idea list, not a work plan.** The inclusion of an idea does not guarantee that it will be picked up by a developer.
{.is-info}

> These ideas can be selected as [eweOS GSoC 2025](https://os-wiki.ewe.moe/activities/gsoc) project proposals.
{.is-success}

## System Utils

### EKMS (DKMS for eweOS)

DKMS is not eweOS-compatible, and a new, eweOS-compatible mechanism needs to be written in order to manage kernel modules.

<details>
  <summary>More Info</summary>

#### Tasks

- Design a manager to build, install and remove kernel modules automatically
- Integrate it with pacman to trigger actions on package operations (kernel upgrades, module package installs/removals).
- Write testing and documentation

#### Expected Outcome

- A fully functional EKMS system that allows eweOS users to easily build, install, and manage kernel modules

#### Required Skills

- POSIX Shell
- C Programming

#### Useful Links

- [DKMS Source Repo](https://github.com/dell/dkms)
- [AKMS Source Repo (alpine's Kernel Module Support)](https://github.com/jirutka/akms)

</details>

### Implement Library API for Turnstile

Systemd integrates systemd-logind to track user sessions and seats, providing both D-Bus API and C API (through libsystemd) for querying these information. Many desktop applications, such as polkit and wireplumber, depend on the API. elogind implements these APIs but it's split from systemd source and thus unreliable and dirty. Without systemd, eweOS integrates turnstile to manage user session and per-session service managers. But it doesn't come with APIs to query these information.

This aims to communicate with the upstream of turnstile (Chimera Linux) and implement a necessary set of APIs to get turnstile supporting most Linux desktop applications. To keep compatible with programs relying on libsystemd/elogind-style API, a wrapper library may be required as well.

<details>
  <summary>More Info</summary>

#### Tasks

- Create related issue in turnstile upstream with the situation explained
- Discuss with turnstile developers, determining the necessary set of APIs 
- Help with the implementation if possible
- Write libraries/daemons to wrap turnstile API into libsystemd-style ones
- Enabling session-related features in eweOS packages as a real-world test against the implementation

#### Expected Outcome

- Well-documented APIs are implemented in turnstile, suitable for usage of real-world Linux programs
- A library serves as compatible layer between sd-login and turnstile APIs
- Disabled features on eweOS due to missing session tracking API get enabled.

#### Required Skills

- C Programming
- Experience with POSIX/Linux APIs
- Execllent communication skills

#### Useful Links

- [Repository of turnstile](https://github.com/chimera-linux/turnstile)
- [Manpage of systemd-logind C API](https://www.man7.org/linux/man-pages/man3/sd-login.3.html)
- [Documentation of ConsoleKit2](https://consolekit2.github.io/ConsoleKit2/)

</details>
  
### GRand Unified Boot Config Generator

GRUB was the old bootloader used by eweOS and Limine has replaced its place. U-boot is another bootloader popular among devboards and we want to support it as well. This aims to implement a generic framework, which evaluates some scripts to check available boot entries and create configuration for them, like `grub-mkconfig`. The difference is that GRUBCG is designed to support multiple different bootloaders.

<details>
  <summary>More Info</summary>

#### Tasks

- Design API to describe boot entires between the framework, the generator backend and scripts for deciding boot entries. 
- Implement backends for U-boot (extlinux.conf) and Limine
- Packaging on eweOS, add appropriate triggers to regenerate boot configuration automatically on system upgrades

#### Expected Outcome

- Well-documented configuration generator with Limine/U-boot support and eweOS integration

#### Required Skills

- Familiar with shell scripts.

#### Useful Links

- [Source of grub-mkconfig](https://github.com/olafhering/grub/blob/master/util/grub-mkconfig.in)
- [(Archived) Configuration Generator for Limine](https://github.com/AnErrupTion/LimineLinuxDeploy)
- [u-boot-menu maintained by Debian](https://salsa.debian.org/debian/u-boot-menu)

</details>
  
## Languages

#### Package openjdk (latest version) on riscv64 and loongarch64

Since there is no pre-compiled version of openjdk for musl for the riscv64/loongarch64 architecture, eweOS has not yet packaged the latest version of openjdk on riscv64/loongarch64. Since openjdk 24 will be released soon, packaging it will predictably require some patches and modifications.

<details>
  <summary>More Info</summary>

#### Tasks

- Upgrade the openjdk in eweOS to the latest version (24).
- Build the latest version of the openjdk for the riscv64/loongarch64 architecture in eweOS.
- (Optional) Upstream related patches if possible.

#### Expected Outcome

- A working openjdk (latest version) on riscv64 for eweOS

#### Required Skills

- C++
- Java
- Software packaging

#### Useful Links

- [Current version (23) of openjdk in eweOS](https://github.com/eweOS/packages/tree/java23-openjdk)

</details>

## Infra

### Improve PKGBUILD Parser in Open Build System

Currently, Open Build Service is used by eweOS as building system. We found its pacman support, especially the PKGBUILD parser implemented in Perl with mostly regex, is quite flaky and lacks of bash features. This aims to improve the PKGBUILD parser to provide better compatibility with ArchLinux-like packaging convention.

<details>
  <summary>More Info</summary>

#### Tasks

- Implement array expansion (`makedepends+=("${_common_deps[@]}")`)
- Implement parameter expansion (`source=("xxx/${pkgver//./_}")`)
- Correctly parse comments in arrays (see useful links)
- Find a way to parse/evaluate dynamic modification to the properties (`[ "$ARCH" = "x86_64" ] && makedepends+=(nasm)`)

#### Expected Outcome

- Implement first three missing features in OBS and upstream the support
- If possible, figure out a solution for dynamic modified properties. This is likely to be hard thus isn't a hard requirement.

#### Required Skills

- pacman packaging experience, knowledge about PKGBUILD format
- Perl programming

#### Useful Links

- [Implementation of PKGBUILD parser in Open Build Service](https://github.com/openSUSE/obs-build/blob/master/Build/Arch.pm)
- [Comments in an array break the parser](https://github.com/eweOS/packages/pull/1082/commits/7e7e99b9cdef8915ebe28e1491ddb41d1a34d163)

</details>
  
#### eweOS User Repository (EUR)

Similar to ArchLinux, eweOS also plans to build a User Repository, which we will call EUR. The difference is that instead of using the AURweb scheme, we want to write our own distributed repo management system, where the code will be hosted in the user's own git repo. This means that we'll also need a corresponding EUR Helper.

<details>
  <summary>More Info</summary>
  
#### Tasks

- Write a workflow for parsing the contents of .SRCINFO and structuring it (e.g. json).
- Write a set of workflows that use the above tools to automatically scan distributed git repositories against a list and update structured data.
- Choose one:
  - Write a set of AURweb-compatible api's to make EUR compatible with the existing AUR Helper.
  - Write a EUR Helper that provide the same basic functionality as the AUR Helper, such as searching, downloading, and building.

#### Expected Outcome

- A usable, auto-refreshing repository of EUR metadata from distributed git repositories.
- Any User Repository helper that works.

#### Required Skills

- GitHub workflow
- python, javascript, bash, or any suitable programming language

#### Useful Links

- [AURweb repo](https://gitlab.archlinux.org/archlinux/aurweb)
- [A proposed draft of EUR design](https://hackmd.io/@yukarichiba/By3uVDW71x)

</details>
  
#### Automatic Testing Infra

eweOS is a relatively small distribution and perfect testing usually means a lot of duplicated work, which isn't practical for our developers. Luckily, OpenQA provides a method to convert manual testing steps into scripts and check the result automatically.

This aims to setup an automatic testing infra based on OpenQA and write corresponding testcases for eweOS, enhancing reliability and reducing manual work.

<details>
  <summary>More Info</summary>

#### Tasks

- Setup an OpenQA x86_64 instance for eweOS
- Write testcases to verify functionalities against tools included in eweOS desktop liveimage.
- Write testcases to perform an installation in eweOS desktop liveimage.
- Write testcases to check the installation works as expected.

#### Expected Outcome

- A suite of testcases to verify functionality of eweOS desktop liveimage.

#### Required Skills

- Perl programming
  
#### Useful Links

- [OpenQA Website](http://open.qa/)

</details>

## Wiki
#### Creating, editing and organizing of wiki content

Currently the eweOS Wiki is still not organised in a neat way and lacks a lot of guidance for users and developers. The lack of guidance on some key steps has led to users having to seek help from community developers to install or configure eweOS, and the lack of documentation has left contributors with no way to get started with eweOS packages, infrastructure, and workflows.

<details>
  <summary>More Info</summary>
  
#### Tasks

- Write guides about eweOS installation on the Wiki
- Write guides about eweOS configuration for a graphical desktop and/or command line environment
- Improve the table of contents and chapter structure of the Wiki.
- Write packaging guidelines for developers on different package topics (e.g. programming languages like Python, Perl, Go, or build tools like CMake or meson).

#### Expected Outcome

- Improvements and contributions to the Wiki as described above

#### Required Skills

- Markdown
- Basics about the system maintenance of Linux distros
- PKGBUILD-based packaging (required to write the wiki for developers)
- One or more programming languages (required to write the wiki for corresponding topics)

#### Useful Links

- [Arch installation guide (Some of this applies to eweOS as well)](https://wiki.archlinux.org/title/Installation_guide)
- eweOS wiki pages on this site

</details>