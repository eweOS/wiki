---
title: Desktop Environments
description: 
published: 1
date: 2024-01-09T02:30:24.234Z
tags: 
editor: markdown
dateCreated: 2023-02-25T04:59:55.067Z
---

Here is a list of packages with official support (or plans to support). Each components would be used in at least one variant of our system images.

# Greeters

Currently we use `greetd` and its greeter implimentations.

|Package|Feature|Support|
|-------|-------|-------|
|`greetd-tui`|CLI|Y(Default CLI Greeter)|
|`greetd-gtk`|GTK3|Y|
|`greetd-regreet`|GTK4|Y|

# Wayland Compositors

|Package|Type|Feature|Support|
|-------|----|-------|-------|
|`wayfire`|Stacking|`wlroots`|Y|
|`sway`|Tiling|`wlroots`|Y|
|`cage`|Kiosk||Y (for greeters)|
|`hyprland`|Tiling|`wlroots`|Y|
|`weston`|Stacking||demo only|

# Desktop Applications

## Status Bars

### waybar

## Wallpaper Managers

### swaybg

### swww

## Application Launchers

### wofi

## Screen Lockers

### swaylock

### gtklock

## Power Menus

### wlogout