---
layout: post
title: Fix DNS no longer work with .local domains (Yosemite)
tags:
  - osx
  - dns
comments: true
---

![_config.yml]({{ site.baseurl }}/images/osx.jpg)

## Problem

Yosemite DNS will no longer work with .local domains, the .local domains was not resolved.

## Solution

Add “orchard.local” to VPN/Advanced/DNS/Search domains AND the Wi-fi/Advanced/DNS/Search domains, the problem is fixed.


Happy Coding! 😇