---
layout: post
title: Set up EPiServer CMS and Commerce with AspNet Identity from scratch
tags:  
  - episerver
  - episerver commerce
comments: true
---

![_config.yml]({{ site.baseurl }}/images/episerver-new.png)
Back to 2015, I wrote a blog post - [Set up EPiServer CMS + Commerce in 11 steps](https://javafun.github.io/set-up-episerver-cms-commerce-in-11-steps/){:target="_blank"} based on Episerver version 9. After 4 years, the setup steps still largely remain the same if you want to use default aspnet membership. Thanks to Episerver product development team great work to keep the platform upgrade and maintain the backward compabilities. 

In this blog post, I will walk you through from beginning on setup CMS Commerce first, then follow by setup identity on both Commerce manager and CMS. If you're already familiar with CMS and Commerce setup, you can skip [Set up CMS project with Commerce](#set-up-cms-project-with-commerce), [Set up Commerce project (Commerce manager)](#set-up-commerce-project-commerce-manager) and jump to [Set up AspNet Identity in Commerce project](#set-up-aspnet-identity-in-commerce-manager-project), [Set up ASpNet Identity in CMS project](#set-up-aspnet-identity-in-cms-project) directly.


* TOC
{:toc}

## Prerequisites

* Visual Studio 2017/2019
* Windows 10 with localdb installed.
* EPiServer CMS VSIX. (You can install within Visual Studio Extension Manager or download from [here](https://marketplace.visualstudio.com/items?itemName=EPiServer.EpiserverCMSVisualStudioExtension){:target="_blank"})


## Getting Started
### Set up CMS project with Commerce
1. Use EPiServer VSIX template to set up an empty CMS project.
![_config.yml]({{ site.baseurl }}/images/episerver-cms-commerce-aspnet-identity/01-create-empty-alloy-website.png)
2. UPDATE all EPiServer packages to latest except `Castle` and `Newtonsoft.Json`.
  >Warning: At the time of writing this blog post, the latest EPiServer.Commerce is 13.10.0, and it has dependecy on EPiServer.Commerce.Core which depends on Newtonsoft.Json (≥ 9.0.1 && < 12.0.0)
  > The EPiServer.CMS.Core has dependency on Castle.Windsor (≥ 4.1.0 && < 5.0.0)
3. Install `EPiServer.Commerce` package into CMS project.
4. Run cmdlet `update-epidatabase`  via nuget package console to update database with all latestes SQL scripts.
5. Login to CMS administrative interface with default credntials, then clicks “execute all pending steps” link to run the migration
  > **username : admin**
  >
  > **password : store**

    ![_config.yml]({{ site.baseurl }}/images/episerver-cms-commerce-aspnet-identity/02-run-migration.png)
6. Once complete the migration, go to verify both CMS and Commerce. 
![_config.yml]({{ site.baseurl }}/images/episerver-cms-commerce-aspnet-identity/03-migration-complete.png)
![_config.yml]({{ site.baseurl }}/images/episerver-cms-commerce-aspnet-identity/04-verify-cms.png)
![_config.yml]({{ site.baseurl }}/images/episerver-cms-commerce-aspnet-identity/05-verify-commerce.png)

### Set up Commerce project (Commerce manager)
8. Create an empty Mvc application with Visual Studio.
  ![_config.yml]({{ site.baseurl }}/images/episerver-cms-commerce-aspnet-identity/06-create-empty-web-application.png){:width="100%"}
9. Install `Episerver.CommerceManager` package into Commerce project.
  ![_config.yml]({{ site.baseurl }}/images/episerver-cms-commerce-aspnet-identity/07-install-commerce-manager.png)
10. Run cmdlet `update-epidatabase` via package manager console.
11. Show all files and include `App_Data`,`App_GlobalResources,Apps`, `NotificationTemplates ` folders and `Default`,`Global.asax`,`EPiServerDefault.aspx`,`EPiServerLog.config` files.
  ![_config.yml]({{ site.baseurl }}/images/episerver-cms-commerce-aspnet-identity/08-inclue-hidden-folder-and-files.png)
12. Make sure “CommerceManagerLink” in CMS is pointing to commerce manager url.

```xml
<add key="CommerceManagerLink" value="http://localhost:{port}/" />
```

### Set up AspNet Identity in Commerce Manager project

1. Install `EPiServer.CMS.UI.AspNetIdentity` package into the Commerce project. 
2. Install `EPiServer.ServiceLocation.StructureMap` package into the Commerce project.
3. Create an Owin startup named [Startup.cs](https://gist.github.com/javafun/a921d94163e327e54154b37de6130b33){:target="_blank"} under root of Commerce project.    
3. Execute the [SQL script](https://gist.github.com/javafun/ab97de51a74b92566f803624d22c3468){:target="_blank"} will create default user `admin@example.com` with password `store` in AspNet Identity table  
4. Create `Overrides` folder under root and create the following web form page/control under Overrides folder. Commerce Manager is a legacy WebForm system, and coupled with old ASP.NET membership provider by default. What we're doing here is to create custom version of login/logut page and later in the code-behind file we can overwrite with AspNet Identity implementation.
  * [Login.aspx](https://gist.github.com/javafun/29837dfdd1caa069908af9df1348eea4#file-login-aspx){:target="_blank"}
  * [Login.aspx.cs](https://gist.github.com/javafun/29837dfdd1caa069908af9df1348eea4#file-login-aspx-cs){:target="_blank"}
  * [Login.aspx.designer.cs](https://gist.github.com/javafun/29837dfdd1caa069908af9df1348eea4#file-login-aspx-designer-cs){:target="_blank"}
  * [Logout.aspx](https://gist.github.com/javafun/ba0340d4cbbcba3e2397cf1d5a3e1990#file-logout-aspx){:target="_blank"}
  * [Logout.aspx.cs](https://gist.github.com/javafun/ba0340d4cbbcba3e2397cf1d5a3e1990){:target="_blank"}
  * [Logout.aspx.designer.cs](https://gist.github.com/javafun/ba0340d4cbbcba3e2397cf1d5a3e1990#file-logout-aspx-designer-cs){:target="_blank"}
  * [MembershipAccountEdit.ascx](https://gist.github.com/javafun/84ef6c4d7e027a78f2549646cca1d35b#file-membershipaccountedit-ascx){:target="_blank"}
  * [MembershipAccountEdit.ascx.cs](https://gist.github.com/javafun/84ef6c4d7e027a78f2549646cca1d35b#file-membershipaccountedit-ascx-cs){:target="_blank"}
  * [MembershipAccountEdit.ascx.designer.cs](https://gist.github.com/javafun/84ef6c4d7e027a78f2549646cca1d35b#file-membershipaccountedit-ascx-designer-cs){:target="_blank"}
  
  ![_config.yml]({{ site.baseurl }}/images/episerver-cms-commerce-aspnet-identity/09-override-files.png)
5. Locate `login.aspx` and `logout.aspx` file under `/Apps/Shell/Pages/` directory, `MembershipAccountEdit.ascx` file under `/Apps/Shell/Customer/Modules`, and update the Page directive with your custom one accordingly.
 ![_config.yml]({{ site.baseurl }}/images/episerver-cms-commerce-aspnet-identity/11-override-login-logout.png) 
  ![_config.yml]({{ site.baseurl }}/images/episerver-cms-commerce-aspnet-identity/12-override-login-logout-2.png)     

6. Add the following `<location>` elements to your Commerce project `web.config`
    ```xml
      <location path="Apps/Shell/Styles">
        <system.web>
          <authorization>
            <allow users="*" />
          </authorization>
        </system.web>
      </location>
      <location path="Apps/Shell/Pages/Login.aspx">
        <system.web>
          <authorization>
            <allow users="*" />
          </authorization>
        </system.web>
      </location>
      <location path="Apps/Shell/EPi/Shell/Light">
        <system.web>
          <authorization>
            <allow users="*" />
          </authorization>
        </system.web>
      </location>  
    ```
> **NOTES**: This step is important, otherwise you'll get infinite redirect loop when access to commerce manager logi.aspx page.

7. Locate `authentication` section in web.config and change mode to `None`
  ![_config.yml]({{ site.baseurl }}/images/episerver-cms-commerce-aspnet-identity/08-authentication-section.png){:width="100%"}
7. Locate `membership` section in web.config and replace with the following 
  ```xml
    <membership>
      <providers>
        <clear />
      </providers>
    </membership>  
  ``` 
8. Locate `roleManager` section in web.config and replace with the following
  ```xml
    <roleManager>
      <providers>
        <clear />
      </providers>
    </roleManager>  
  ```

### Set up AspNet Identity in CMS project

1. Create an Owin startup named [Startup.cs](https://gist.github.com/javafun/dccbbf0c22bd5dbb0902da4e622a09a6){:target="_blank"} under root of CMS project.    
2. Locate `authentication` section in web.config and change mode to `None`  
3. Locate `membership` section in web.config and replace with the following 
  ```xml
    <membership>
      <providers>
        <clear />
      </providers>
    </membership>  
  ``` 
4. Locate `roleManager` section in web.config and replace with the following
  ```xml
    <roleManager>
      <providers>
        <clear />
      </providers>
    </roleManager>  
  ```


It’s the end, and that’s all you need to do for the setup. Enjoy your Episerver development with ASPNET Identity.

## References
* [Set up EPiServer CMS + Commerce in 11 steps](https://javafun.github.io/set-up-episerver-cms-commerce-in-11-steps/){:target="_blank"}
* [EPiServer CMS UI AspNetIdentity OWIN authentication](https://world.episerver.com/documentation/developer-guides/CMS/security/episerver-aspnetidentity/){:target="_blank"}

Happy Coding! 😇