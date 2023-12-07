---
title: Automatic Workflow
description: 
published: 1
date: 2023-12-07T04:00:19.323Z
tags: 
editor: markdown
dateCreated: 2023-05-22T06:27:51.050Z
---

# Build System Automation

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