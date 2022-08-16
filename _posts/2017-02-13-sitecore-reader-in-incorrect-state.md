---
layout: post
title: Sitecore – Reader is in incorrect state
tags:  
  - sitecore
comments: true
---

![_config.yml]({{ site.baseurl }}/images/sitecore.png)
My demo app came up with this issue after making some changes to patch config file today.
<!--more-->
> Reader is in incorrect state 
> Description: An unhandled exception occurred during the execution of the current web request. Please review the stack trace for more information about the error and where it originated in the code.

> Exception Details: System.Exception: Reader is in incorrect state

> Source Error:

> An unhandled exception was generated during the execution of the current web request. Information regarding the origin and location of the exception can be identified using the exception stack trace below.

> Stack Trace:
[Exception: Reader is in incorrect state]
Sitecore.Xml.Patch.XmlReaderSource..ctor(XmlReader reader, String sourceName) +123
Sitecore.Configuration.ConfigPatcher.GetXmlElement(XmlReader reader, String sourceName) +45
Sitecore.Configuration.ConfigPatcher.ApplyPatch(TextReader patch, String sourceName) +138
Sitecore.Configuration.ConfigPatcher.ApplyPatch(String filename) +93
Sitecore.Configuration.ConfigReader.LoadAutoIncludeFiles(ConfigPatcher patcher, String folder) +177


This is a weird issue at the first glance, I still have no idea what happened under the hood, though I solved the problem.

## Cause
<span style="color:red">**I accidentally added a comment in my patch config which is in between and section, this is the fundamental cause.**</span>

## Solution
To fix this YSOD, simply move the comment anywhere within section.

Happy Coding! 😇