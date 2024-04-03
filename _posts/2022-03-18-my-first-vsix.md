---
layout: post
title: My first Visual Studio 2022 extension
tags:
  - optimizely
  - optimizely cms
  - Optimizely content cloud
  - Optimizely commerce cloud
  - VSIX
comments: true
# pin: true
image:
  path: /images/optivsix/image.png
---

<!-- ![_config.yml]({{ site.baseurl }}/images/optivsix/image.png) -->

I start using Visual Studio 2022 for my development more frequently this year, especially working on ASP.NET Core project. One of my main pain points to use the newer version of any software is to find the alternative / replacement of something that I'm familiar with. This is extremely important to me as it will impact my productivity a lot.

<!--more-->

To ensure moving to Visual Studio 2022 successfully, I need to have all my favorite extensions working. Unfortunately, this isn't the case for me this time as one of my favorite extension for Optimizely (formerly Episerver) development hasn't provided update to support for Visual Studio 2022.

I decide to take this opportunity and use my spare time to create my first extension - [Optimizely Content and Commerce Cloud Templates](https://marketplace.visualstudio.com/items?itemName=VincentYang024.OptiVS2022Tooling).

> NOTE: This extension apparently can only be installed on Visual Studio 2022, and the templates are designed for CMS 12 / Commerce 14.

## Features

- Create content types (page, block and media)
- Create page type controller
- Create block and async block component
- Create InitializationModule
- Create SchedulerJob
- Code snippet for quickly creating property - optiprop

## Demo

### Create new template

<img src="https://vincentyang024.gallerycdn.vsassets.io/extensions/vincentyang024/optivs2022tooling/1.0.0/1646884891629/cms-template__1.gif"/>

### Create new property

<img src="https://vincentyang024.gallerycdn.vsassets.io/extensions/vincentyang024/optivs2022tooling/1.0.0/1646884891629/codesnippet.gif"/>

## How can I help?

If you enjoy using the extension, please give it a ★★★★★ rating on the Visual Studio Marketplace.

## References

[Start developing extensions in Visual Studio](https://docs.microsoft.com/en-us/visualstudio/extensibility/starting-to-develop-visual-studio-extensions?view=vs-2022)

[https://devblogs.microsoft.com/visualstudio/writing-extensions-just-got-easier/](https://devblogs.microsoft.com/visualstudio/writing-extensions-just-got-easier/)

Happy Coding! 😇
