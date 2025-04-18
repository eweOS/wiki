---
title: Vulkan / SPIR-V
description: Vulkan / Standard Portable Intermediate Representation
published: 1
date: 2025-04-18T03:35:34.524Z
tags: 
editor: markdown
dateCreated: 2023-12-13T07:28:01.659Z
---

# Current Version

current vulkan sdk version: 1.4.309.0

## Order 0
- `vulkan-headers`: `vulkan-sdk-${vulkan-headers}`
- `spirv-headers`: `vulkan-sdk-${vulkan-headers}`

## Order 1
- `spirv-tools`: `vulkan-sdk-${vulkan-headers}`
- `vulkan-volk`: `vulkan-sdk-${vulkan-headers}`
- `vulkan-icd-loader`: `vulkan-sdk-${vulkan-headers}`

## Order 2
- `spirv-llvm-translator`: 18.1.4 (18.1.4 for `llvm`)
- `glslang`: 15.2.0

## Order 3
- `libclc`: 18.1.4 (same as `llvm`)
- `vulkan-tools`: `vulkan-sdk-${vulkan-headers}`
- `shaderc`: 2024.4