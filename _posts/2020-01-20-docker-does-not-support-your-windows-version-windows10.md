---
layout: post
title: Docker doesn't support your windows version
tags:
  - docker
comments: true
image:
  path: /images/docker.png
---

<!-- ![_config.yml]({{ site.baseurl }}/images/docker.png) -->

Today, I receive an update after start docker on my laptop. After update finish, I encounter `Docker doesn't support your windows version. Check documentation for minimum requirements` error.

<!--more-->

<img src="/images/docker-does-not-support/docker-does-not-support-windows-version-error.png" width="600" style="display:block"/>

## Causes

After search on the internet, I found other people had the same issue after update to latest docker client and raised on [docker-for-win](https://github.com/docker/for-win/issues/4482). The current issue status has been marked closed, however I don't see any pull request link to address this issue. Luckily, I found the workaround by going through the discussion in the thread.

The root cause of this issue is my machine `PSModulePath` environment variable got messed up. The entry for `C:\Windows\System32\WindowsPowerShell\v1.0\Modules` was replaced with text `System.String[]`

<img src="/images/docker-does-not-support/env-variable-mess-up.png" width="700" style="display:block"/>
<img src="/images/docker-does-not-support/env-variable-mess-up-2.png" width="400" style="display:block"/>

## Fixes

The fix is very simple. Open _Environment variables_, edit `PSModulePath` variable under _System variables_ section and replace `System.String[]` to `C:\Windows\System32\WindowsPowerShell\v1.0\Modules`.
<img src="/images/docker-does-not-support/env-variable-fix.png" width="400" style="display:block"/>

Launch docker from start menu, my docker is back and running. Hooray!!

## References

N/A

Happy Coding! 😇
