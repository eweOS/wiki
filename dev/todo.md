---
title: TODO
description: A list of TODOs
published: 1
date: 2024-01-05T09:56:21.908Z
tags: 
editor: markdown
dateCreated: 2023-02-25T04:24:22.548Z
---

## Build System

- [x] Add aarch64 workers
- [x] Add riscv64 workers

## System Image

- [ ] Create bootable Disk Image for AArch64
- [x] Create bootable Live CD Image
  - [x] Within eweOS
- [x] Create bootable ISO Image
  - [x] Within eweOS
- [ ] Compile EFI stub instead of use binary file
- [x] Create bootable image with desktop support

## Hardware / Architecture

- [x] Split linux-firmware package
- [x] Add initial support for RISC-V

## System Utils

- [ ] [Replace busybox](/dev/todo/replace-busybox)
- [ ] catnest: hook to reload
- [ ] pawprint: hook to reload
- [x] dinit: redesign system services
- [x] dinit: add user services

## Languages

- [ ] Bootstrap basic Python package groups
- [ ] Bootstrap basic Java package groups

## Desktop

- [x] Audio Playback Support
	- [x] wireplumber
  - [x] pipewire-pulse
  - [x] alsa-libs
- [ ] Branding
	- [ ] Default wallpapers
  - [ ] Artwork resources
- [ ] Add standalone session for eweOS
  - [ ] choose a default compositor

## Optimization

- [x] Enable default LTO
- [x] Enable default mimalloc

## Infra

- [x] [Version Bumper](/dev/todo/version-bumper)
- [ ] keyring

## Wiki

- [x] Page to list all eweOS github projects