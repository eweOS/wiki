---
title: Vulkan / SPIR-V
description: Vulkan / Standard Portable Intermediate Representation
published: 1
date: 2024-04-23T06:07:06.060Z
tags: 
editor: markdown
dateCreated: 2023-12-13T07:28:01.659Z
---

# Current Version

## Order 0
- `vulkan-headers`: 1.3.280
- `spirv-headers`: 1.3.280.0

## Order 1
- `spirv-tools`: 2024.1+1.3.280.0 (sdk-1.3.280.0 for `spirv-headers`)
- `vulkan-icd-loader` (1.3.280 for `vulkan-headers`)

## Order 2
- `spirv-llvm-translator`: 18.1.0 (18.1.0 for `llvm`)
- `glslang`: 14.1.0

## Order 3
- `libclc`: 18.1.4 (same as `llvm`)