---
title: Automatic Workflow
description: 
published: 1
date: 2024-04-29T09:10:45.937Z
tags: 
editor: markdown
dateCreated: 2023-05-22T06:27:51.050Z
---

# GitHub Automations

## Update Checker Automation

> cron: '0 0 * * *'
{.is-info}

container: `ghcr.io/eweos/docker:updatecheck`

## PR Automation

> webhook: New PR
{.is-info}

container:
- namcap: `archlinux:latest`
- build: `ghcr.io/eweos/docker:buildenv`

## Docker Image Creation

> cron: '0 0 * * *'
{.is-info}

container:
- `master`: `ghcr.io/eweos/docker:master`
- `buildenv`: `ghcr.io/eweos/docker:master-->buildenv`
- `updatecheck`: `ghcr.io/eweos/docker:master-->updatecheck`

## ISO Image Creation

> cron: '0 0 */3 * *'
{.is-info}

location: https://github.com/eweOS/iso/actions

## Update list of packages

> cron: '0 0 * * *'
{.is-info}

location: `https://github.com/eweOS/workflow/tree/pkginfo-$arch`

# Repository Automations

## Build System --> Sync Server

## Sync Server --> Official Mirror

## Image Build System --> Official Mirror