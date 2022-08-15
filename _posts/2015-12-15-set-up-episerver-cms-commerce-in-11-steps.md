---
layout: post
title: Set up EPiServer CMS + Commerce in 11 steps
tags:  
  - episerver
  - episerver commerce
comments: true
---

![_config.yml]({{ site.baseurl }}/images/episerver-new.png)
Believe or not, it’s super easy to set up an empty CMS site with Commerce package in version 9. Thanks for the EPi team awesome work. In this post, I will walk you through step by step how easy to set up Commerce in EPiServer from scratch.

## Prerequisites

* Visual Studio 2013/2015
* Windows 8 above (At least, you will need to have localdb installed.)
* EPiServer CMS VSIX. (You can install within Visual Studio Extension Manager or download from [here](https://marketplace.visualstudio.com/items?itemName=EPiServer.EpiserverCMSVisualStudioExtension))

## Getting start

#### CMS

1. Use EPiServer VSIX template to set up an empty CMS project.
  > ![_config.yml]({{ site.baseurl }}/images/epi-cms-commerce/11.png)
  >
  > ![_config.yml]({{ site.baseurl }}/images/epi-cms-commerce/2.png)
2. Install package “EPiServer.Commerce.UI.ManagerIntegration”  via nuget package console.
3. UPDATE ALL EPiServer packages.
4. Install package “EPiServer.Commerce”
5. Run cmdlet “update-epidatabase”  via nuget package console.
6. Change local database location – Move database to db folders.
In this demo, I placed the db out side of the CMS directory, and put it in the solution root directory.
```csharp
  static EPiServerApplication()
  {
      System.IO.DirectoryInfo dir = new System.IO.DirectoryInfo(AppDomain.CurrentDomain.BaseDirectory + @"\..\db\");
  AppDomain.CurrentDomain.SetData("DataDirectory", dir.FullName);
  }
```
7. Login to CMS administrative interface with default credntials, then clicks “execute all remaining steps” link to run the migration
  > **username : admin**
  >
  > **password : store**

#### Commerce
8. Create an empty Mvc application with Visual Studio (Framework > 4.5.2)
9. Install the nuget package “Episerver.CommerceManager”.
10. Run cmdlet update-epidatabase
11. Show all files and include App_Data,App_GlobalResources,Apps, NotificationTemplates folders and Default,Global.asax files.
12. Make sure “CommerceManagerLink” in CMS is pointing to commerce manager url.

```xml
<add key="CommerceManagerLink" value="http://localhost:{port}/" />
```


It’s the end, and that’s all you need to do for the setup. Enjoy your EPi development.

Happy Coding! 😇