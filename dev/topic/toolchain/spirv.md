---
title: Vulkan / SPIR-V
description: Vulkan / Standard Portable Intermediate Representation
published: 1
date: 2024-02-21T09:48:47.823Z
tags: 
editor: markdown
dateCreated: 2023-12-13T07:28:01.659Z
---

# Current Version

## Order 0
- `vulkan-headers`: 1.3.262
- `spirv-headers`: 1.3.261.1

## Order 1
- `spirv-tools`: 2023.3+1.3.261.1 (sdk-1.3.261.1 for `spirv-headers`)
- `vulkan-icd-loader` (1.3.262 for `vulkan-headers`)

## Order 2
- `spirv-llvm-translator`: 17.0.0 (17.0.0 for `llvm`)
- `glslang`: 13.1.1

## Order 3
- `libclc`: 17.0.6 (same as `llvm`)