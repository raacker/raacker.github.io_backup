---
layout: post
title: "inttypes.h"
date: "2016-09-25 23:56:23 +0900"
location: "Daejeon, South Korea"
category: C
tags: [til, neovim, opensource, c]
---

sometimes, device dependency makes hard to use data types. If a device uses 32-bit, void* becomes 32-bit also. But If it uses 64-bit, also followed.

Using inttypes.h makes these things done.

if you need to print out int64_t in decimal,
printf("%" PRId64, val)

if  you need to print out int64_t in hexadecimal,
printf("%" PRIx64, val)

need to print address value?
printf("%" PRIdPTR, val)

in hexadecimal?
printf("%" PRIxPTR, val)
