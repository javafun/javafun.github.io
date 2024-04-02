---
layout: post
title: Umbraco - uSyn Content Disable Content Sync
tags:
  - umbraco
  - umbraco 7.12.4
comments: true
image:
  path: /images/umbraco.png
---

<!-- ![_config.yml]({{ site.baseurl }}/images/umbraco.png) -->

By default, after you install the `uSync Content Edition` nuget package, it will enable the content sycn (both content and media).

<!--more-->

To disable the auto content sycn, locate file `uSyncBackOffice.Config` under `config` folder, and set the following handler to false.

```xml
    <HandlerConfig Name="uSync: ContentHandler" Enabled="false" />
    <HandlerConfig Name="uSync: MediaHandler" Enabled="false" />
```

Happy Coding! 😇
