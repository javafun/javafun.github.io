---
layout: post
title: CQ Clientlibs debug tips
tags:
  - adobe cq
comments: true
image:
  path: /images/adobecq.jpg
---

<!-- ![_config.yml]({{ site.baseurl }}/images/adobecq.jpg) -->

<!--more-->

## Clientlibs

1. Clientlibs depen­den­cies console
   http://localhost:4502/libs/granite/ui/content/dumplibs.html

2. Rebuild clientlibs
   http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html

3. Debug clientlibs
   Append ?debugClientLibs=true to write out single file and CTRL+SHIFT+U gives you tim­ing info.

## Where are the gen­er­ated files stored in CQ?

They are in **/var/clientlibs**

## When devel­op­ing I want to have sin­gle file ref­er­ences in my HTML

Enable the debug-option in the HTML Library Manager

## How can I use cache-busting and clientlibs?

You can enable the hash­ing of the url via ‘[ver­sioned clientlibs](https://adobe-consulting-services.github.io/acs-aem-commons/features/versioned-clientlibs/index.html)’.

## To see a “final View” of your test page without to publish: wcmmode=disabled

http://localhost:4502/cf#/content/geometrixx/folder/test.html?wcmmode=disabled

## Reference

- Clientlibs explained by example
  http://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/
- Using Client-Side Libraries
  https://docs.adobe.com/docs/en/cq/5-6-1/developing/clientlibs.html

Happy Coding! 😇
