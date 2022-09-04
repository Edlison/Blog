---
title: Unauthorized UEFI shows up when booting
categories:
- Error
tags:
- boot
---

# Intro

无法自动引导到系统

# Solution

1. 进入BIOS的Advanced mode
2. security mode中将windows改为other

好像是由于在判断是否为授权的WindowsUEFI

更改过后就可以通过UEFI引导系统了, 之前只能通过Legacy引导.





----

Reference

https://blog.csdn.net/qq_36651243/article/details/93850901