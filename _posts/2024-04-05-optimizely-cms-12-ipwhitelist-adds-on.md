---
layout: post
title: IP Whitelist Add-on for Optimizely CMS 12
tags:
  - optimizely
  - optimizely cms
  - optimizely cms 12
comments: true
image:
  path: /images/cms_with_app.png
---

<!-- ![_config.yml]({{ site.baseurl }}/images/cms_with_app.png) -->

Recentlly, I have been working on a new CMS 12 module - **IP Whitelist** and I finally make it available on the [nuget.org](https://www.nuget.org/packages/IPWhitelist/){:target="\_blank"}.

<!--more-->

The primary goal of this module is to simplify the environment access control for customers/partners during the development phase especially for rebranding projects as clients usually do not want to disclose their new brand/designs before it goes live.

This module is **free** and designed for blocking/restricting access on a per site basis for `Optimizely CMS 12+` solution hosted on Optimizely DXP with the following features

- Fully multi-site supports.
- Whitelist single IP address.
- Whitelist a range of IP addresses using Classless Inter-Domain Routing (CIDR).
- Whitelist known paths (e.g. /episerver/health)

## Interfaces

### IP screenshot

<img src="/images/ipwhitelist/ip.png"/>

<br/>
<br/>

### CIDR screenshot

<img src="/images/ipwhitelist/cidr.png"/>
<br/>
<br/>

### Ignore Path(s) screenshot

<img src="/images/ipwhitelist/ignore_path.png"/>

## Installation & Configuration

**Startup.cs**

After installing the package IPWhitelist in your project, you need to ensure the following lines are added to the `startup.cs` class of your solution:

```csharp
public void ConfigureServices(IServiceCollection services)
{
   // .... other services

   services.AddIpWhitelist();
}

public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    // Add IPWhitelist middleware before any other middleware
    app.UseIpWhitelist();
    // ... other middleware
}
```

The call to services.AddIpWhitelist() sets up the dependency injection required by the IPWhitelist to ensure the solution works as intended. This works by following the Services Extensions pattern defined by Microsoft.

## Documentation

Details can be found [here](https://github.com/vyan024/IpWhitelistAddonDoc){:target="\_blank"}. If you encounter any issue, feel free to raise the issue there.

<img src="/images/ipwhitelist/create_issue.png"/>

## Limitations

- This module is **NOT** designed to work with `Optimizely CMS 11` or below.

## Support

IPWhitelist is a free module. If you like this module and keen to support me, you can get me a coffee 😃

<a href="https://www.buymeacoffee.com/javafun"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a coffee&emoji=☕&slug=javafun&button_colour=FF5F5F&font_colour=ffffff&font_family=Comic&outline_colour=000000&coffee_colour=FFDD00" /></a>

Happy Coding! 😇
