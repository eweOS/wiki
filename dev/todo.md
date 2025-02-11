---
title: TODO
description: A list of TODOs
published: 1
date: 2025-02-11T13:15:49.515Z
tags: 
editor: markdown
dateCreated: 2023-02-25T04:24:22.548Z
---

> **This is an idea list, not a work plan.** The inclusion of an idea does not guarantee that it will be picked up by a developer.
{.is-info}

## System Image

## Hardware / Architecture

## System Utils

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

## Desktop

**Creation of Desktop Artwork**

<details>
  <summary>More Info</summary>
  
  

</details>

## Optimization

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

<details>
  <summary>More Info</summary>
  
  

</details>
  
#### Automatic Testing Infra

eweOS is a relatively small distribution and perfect testing usually means a lot of duplicated work, which isn't practical for our developers. Luckily, OpenQA provides a method to convert manual testing steps into scripts and check the result automatically.

This aims to setup an automatic testing infra based on OpenQA and write corresponding testcases for eweOS, enhancing reliability and reducing manual work.

<details>
  <summary>More Info</summary>

#### Tasks

- Setup an OpenQA x86_64 instance for eweOS
- Write testcases to verify functionalities against tools included in eweOS desktop image.
- Write testcases to perform an installation in eweOS desktop image.
- Write testcases to check the installation works as expected.

#### Expected Outcome

- A suite of testcases to verify functionality of eweOS desktop liveimage.

#### Required Skills

- Perl programming
  
#### Useful Links

- [OpenQA Website](http://open.qa/)

</details>

## Wiki

**Creating, editing and organizing of wiki content**



<details>
  <summary>More Info</summary>
  
  

</details>