---
layout: post
title: How to get pagetype’s AvailablePageTypes programatically?
tags:
  - episerver
comments: true
image:
  path: /images/episerver.png
---

<!-- ![_config.yml]({{ site.baseurl }}/images/episerver.png) -->

<!--more-->

## Find page type’s available types

```csharp
IAvailablePageTypes availablePageTypes = ServiceLocator.Current.GetInstance<IAvailablePageTypes>();
AvailableSetting setting = availablePageTypes.GetSetting(this.Name);
IList<string> allowedPageTypeNames = setting.AllowedPageTypeNames;
```

If you need more information about your available Page Types you can do:

```csharp
PageTypeRepository repository = ServiceLocator.Current.GetInstance<PageTypeRepository>();
IEnumerable<PageType> availablePageTypes = allowedPageTypeNames.Select(name => repository.Load(name));
```

You have to use `include` property not `includeon` property on your page type, otherwise you will not be able to get any result from GetSetting method.

## Resources

http://world.episerver.com/Modules/Forum/Pages/Thread.aspx?id=72917&epslanguage=en
http://cjsharp.com/blog/2013/04/11/a-closer-look-at-the-availablepagetypes-attribute-in-episerver-7/

Happy Coding! 😇
