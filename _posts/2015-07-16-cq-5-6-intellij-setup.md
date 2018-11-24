---
layout: post
title: CQ 5.6 IntelliJ Setup
tags:
  - intellij 14
  - adobe cq
comments: true
---

![_config.yml]({{ site.baseurl }}/images/intellij.png)

Follow the link below to if you set up a project from scratch https://github.com/javafun/CQ561_POM#purpose–demonstration 

If the intellisense doesn’t work, make sure you have included the following artifact in the POM.xml

* com.day.cq.wcm
* cq-wcm-taglib

You also need to include the cq taglib prefix and

![_config.yml]({{ site.baseurl }}/images/intellij-debugcq/snip20150716_7.png)

You also need to make sure the pom file marked as Maven project. 

Happy Coding! 😇