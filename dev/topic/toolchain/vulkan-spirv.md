---
title: Vulkan / SPIR-V
description: Vulkan / Standard Portable Intermediate Representation
published: 1
date: 2024-09-03T02:45:43.585Z
tags: 
editor: markdown
dateCreated: 2023-12-13T07:28:01.659Z
---

# Current Version

## Order 0
- `vulkan-headers`: 1.3.290
- `spirv-headers`: 1.3.290.0

## Order 1
- `spirv-tools`: 2024.3+1.3.290.0 (sdk-1.3.290.0 for `spirv-headers`)
- `vulkan-icd-loader` (1.3.290 for `vulkan-headers`)

## Order 2
- `spirv-llvm-translator`: 18.1.4 (18.1.4 for `llvm`)
- `glslang`: 14.3.0

## Order 3
- `libclc`: 18.1.4 (same as `llvm`)