---
title: eweOS Desktop Environment
description: 
published: 1
date: 2024-05-26T13:23:44.267Z
tags: 
editor: markdown
dateCreated: 2024-03-19T06:33:26.157Z
---

# About

eweOS DE consists of multiple wayland applications/libraries/tools.
Most of them are preinstalled in live ISO.

# Packages

## Core Packages

- `hyprland`: as compositor.
- `dbus`: it's dbus.
- `greetd-regreet`: as greeter.
- `gtklock`: as screen lock.

### audio

- `pipewire`: as audio server.
- `pipewire-pulse`: as pulseaudio server.

### icon

- `papirus-icon-theme`: as icon theme.

### network

- `connman`: as network manager

## Applications

### desktop and widgets

- `rofi`: as popup launcher
- `waybar`: as system-wide toolbar.
- `swww`: as wallpaper manager.

### notification

- `mako`: as notification daemon.

### terminal

- `foot`: as terminal.

### browser

- `firefox`: as browser

### input method

- `fcitx5`: as input method framework
- `fcitx5-chinese-addons`: as Chinese input method framework

### screenshot

> all-in-one command: `grim -g "$(slurp)" - | swappy -f -`

- `slurp`: to select part of screen
- `grim`: to do the screenshot
- `swappy`: to edit screenshot

### monitor management

- `wdisplays`: for GUI
- `kanshi`: for daemonized monitor configuration

# Configurations

WIP

# Packaged out-of-box configuration

WIP