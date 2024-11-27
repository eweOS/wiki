---
title: Desktop Environments
description: 
published: 1
date: 2024-11-27T04:14:49.218Z
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
|`labwc`|Stacking|`wlroots`|Y|
|`sway`|Tiling|`wlroots`|Y|
|`cage`|Kiosk||Y (for greeters)|
|`hyprland`|Tiling||Y|
|`weston`|Stacking||demo only|

# Desktop Environments

## LXQt

### Install

- install group: `lxqt`
- install package: `lxqt-wayland-session`
- install package: any compatible compositor (`labwc` recommended)

### Support Status

## Xfce

### Install

- install group: `xfce4`
- install group: `xfce4-goodies` (Optional, recommended)
- install package: any compatible compositor (`labwc` recommended)

### Support Status

- base runtime
  - libxfce4windowing
  - libxfce4util
  - libxfce4ui
  - xfce4-dev-tools

- group `xfce4`
  - exo
  - garcon
  - thunar: needs patch to remove x11
  - ~~thunar-volman~~
  - ~~tumbler~~
  - xfce4-appfinder
  - xfce4-panel
  - ~~xfce4-power-manager~~: no upower
  - xfce4-session
  - xfce4-settings
  - xfce4-terminal
  - xfconf
  - xfdesktop
  - ~~xfwm4~~: no x11
  - ~~xfwm4-themes~~: no x11

# Standalone Desktop Applications

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