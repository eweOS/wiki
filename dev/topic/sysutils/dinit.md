---
title: dinit
description: 
published: 1
date: 2023-11-27T06:01:31.148Z
tags: 
editor: markdown
dateCreated: 2023-11-24T01:41:21.463Z
---

# bootflow

```plantuml
@startuml

state single #lightblue: Single User Mode (recovery)
state early_detect: Detect running env
state early_mount: Mount /proc /sys ...
state early_cgroups: Mount cgroups
state early_pre.target: Basic env for early stages
state mdev: Mount and expand /dev
state early_modules: Probe kernel modules
state early_devices.target: Essential devices are detected
state early_rootrw: Set root partition to be writable
state early_fs.target: All essential local filesystems are mounted
state early_fstab: Read and mount /etc/fstab
state early_net: Setup lo interface and init network config
state early_hostname: Read /etc/hostname and set hostname
state early_tty: Spawn tty on serial port
state early_sysctl: Read and apply /etc/sysctl.conf
state pawprint: Generate tmpfiles
state catnest: Generate initial users/groups
state utmpd: User status log service
state wtmpd: User status log service
state early_sysutils: All sysutils are loaded and running
state syslogd: System logging daemon
state early_console.target: Early console is spawned and showed up
state early.target: Early stage initialization is completed
state rc.target: Run startup scripts
state network.target: Network initialization is completed
state dbus #white: dbus (system session)
state udhcpc #white: DHCP service
state elogind #white: Session manager
state ntpd #white: Network time sync
state greetd #white: Greeter
state login.target: System is now prepared for user to login
state system: All system services are launched
state boot: All services are launched
state boot.d #lightgrey: All services in /etc/dinit.d/boot.d 
state system.boot.d #lightgrey: All services in /usr/lib/dinit/system/boot.d


[*] --> single
single --> [*]
[*] --> early_detect
early_detect --> early_mount
early_mount --> early_cgroups
early_detect --> early_cgroups
early_detect --> early_pre.target
early_mount --> early_pre.target
early_cgroups --> early_pre.target
early_pre.target --> early_rootrw
early_pre.target --> early_modules
mdev --> early_devices.target
early_pre.target --> mdev
early_modules --> mdev
early_devices.target --> early_hostname
early_devices.target --> early_net
early_devices.target --> early_fstab
early_rootrw --> early_fstab
early_rootrw --> early_fs.target
early_fstab --> early_fs.target
early_devices.target --> early_fs.target
early_fs.target --> syslogd
early_fs.target --> pawprint
early_fs.target --> early_sysctl
early_devices.target --> early_sysctl
early_fs.target --> early_tty
early_devices.target --> early_tty
early_tty --> early_console.target
early_fs.target --> catnest
early_fs.target --> utmpd
early_fs.target --> wtmpd
catnest -> utmpd
catnest --> wtmpd
pawprint --> utmpd
pawprint --> wtmpd
catnest --> early_sysutils
pawprint --> early_sysutils
syslogd --> early_sysutils
utmpd --> early_sysutils
wtmpd --> early_sysutils
early_console.target --> early.target
early_net --> early.target
early_hostname --> early.target
early_sysutils --> early.target
early_fs.target --> early.target
early_sysctl --> early.target
early.target --> rc.target
rc.target --> network.target
rc.target --> login.target
rc.target --> udhcpc
udhcpc -[dotted]-> network.target
rc.target --> ntpd
network.target --> ntpd
ntpd -[dotted]-> login.target
network.target --> system
login.target --> system
system --> boot
rc.target --> dbus
dbus -[dotted]-> login.target
dbus --> elogind
elogind -[dotted]-> login.target
rc.target --> greetd
elogind --> greetd
greetd -[dotted]-> login.target
system.boot.d --> system
boot.d --> boot

@enduml
```

# System Services

## Early Services

## Ordinary Services

# User Services
