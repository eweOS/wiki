---
title: New Build System
description: 
published: 1
date: 2023-05-30T20:53:22.042Z
tags: 
editor: markdown
dateCreated: 2023-05-30T20:53:22.042Z
---

New Build System (currently does not have a codename) for eweOS is now testing and will replace OBS in the future.

# Architecture

## Message Queue

We use `rabbitmq` to provide message queue service for our builders.

- Exchanges:
	- `dispatch`: Read `arch` in headers
  - `dispatch.all` (Internal): Deliver tasks for `all/any` in `arch`, broadcast to all queues
- Queues:
  - `dispatch-{$arch}`: Deliver tasks for each architecure
  
## Builder

There are three types of builders:

- `nspawn`: Use `systemd-nspawn` to create builder containers.
- `docker`: Use `docker run` to create builder containers.
- `chroot`: Use `mount && chroot` to create builder sysroots.

Builders have a 2-stage workflow to ensure all dependencies are installed and all packages are up to date:

- Stage 1: `pacman -Syu` and install/upgrade `base-devel` and `rsync`. Changes are persistent.
- Stage 2: Execute `makepkg` with auto dependency installation enabled. Buildroots are mounted with tmpfs/ramdisk. Sysroots are mounted as read-only with tmpfs overlayfs.

Logs and packages will be uploaded to repo servers automatically if rsync credentials are provided.

Build status of packages will be modified by requesting API when related credentials are provided.

## Update Checker


## Dispatcher

### GitHub Commit Flow

### GitHub PR Flow

### Manually Trigger

## Packages Status API

### Info API

### Update Submission API

### Build Submission API

### Manually Package Creation

## Repo Server

### rsync service

### repo database