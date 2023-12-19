---
title: Repository Management
description: 
published: 1
date: 2023-12-19T06:27:07.760Z
tags: 
editor: markdown
dateCreated: 2023-12-19T06:08:50.393Z
---

# Repositories

## `main` repo

Location: `/eweos/main`
Managed by: `PackageManagers`

This repository provides packages maintained by developers of eweOS team and ready for users.

## `testing` repo

Location: `/eweos/testing`
Managed by: `PackageManagers`

This repository provides unstable/transitional packages in testing stage. Default `pacman.conf` disables this repository and should only enable for developers.

## `eur` repo

Location: `/eweos/eur`
Managed by: `Members`

This repository is maintained by users in eweOS community and only provides `PKGBUILD` with source files instead of binaries to avoid potential legal issues.

## device/platform specific repos

Location: `<TODO>`
Managed by: `PackageManagers`

These repositories is maintained by developers of eweOS team to provide device/platform-specific packages and/or customized packages optimized for specific devices/platforms.

## ports repos

Location: `/eweos-ports/<arch>/{main,testing}`
Managed by: `PortManagers`

These repositories should not be regarded as parts of eweOS repositories since extra architectures are not officially supported by eweOS. However, eweOS allows users to apply for submitting extra architectures maintained by themselves and request eweOS official repo servers to serve these repositories.

# Repo Servers

## Sync Workflow


```plantuml
@startuml

state build_system #lightblue: eweOS Build System
state repo_build_system #lightblue: Repo of build system
state repo_rsync_main #white: Official Rsync server (Main)
state repo_rsync_backup #white: Official Rsync server (Backup)
state repo_official_main: Official repo server (main)
state repo_official_backup: Official repo server (backup)
state repo_community_tier1: Repo of community repo server (tier 1)
state repo_community_tier2: Repo of community repo server (tier 2)
state repo_snapshot: Snapshot repo server

build_system --> repo_build_system
repo_build_system --> repo_rsync_main
repo_build_system --> repo_rsync_backup
repo_build_system --> repo_snapshot
repo_rsync_main --> repo_official_main
repo_rsync_backup -[dotted]-> repo_official_main
repo_rsync_main --> repo_official_backup
repo_rsync_backup -[dotted]-> repo_official_backup
repo_rsync_main --> repo_community_tier1
repo_rsync_backup -[dotted]-> repo_community_tier1
repo_community_tier1 --> repo_community_tier2
repo_snapshot -[dotted]-> repo_community_tier1

@enduml
```

## Rsync Server

## Official Repo Server

## Community Repo Server

### Community Tier 1 Repo Server

### Community Tier 2 Repo Server

## Snapshot Repo Server