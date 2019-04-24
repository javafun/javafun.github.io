---
layout: post
title: How to enable Episerver new and beta features
tags:
  - episerver
  - beta feature
  - episerver commerce
comments: true
---

![_config.yml]({{ site.baseurl }}/images/episerver.png)
As you might know already, Episerver has introduced continuous release process to help the customer quickly get the issue fixed and adopt the new/beta features.

By default, some of these features are required to be manually turned on E.g. SerializedCarts. When it's a beta feature, you'll need to ensure the user are in the right user groups as well. This blog post will help you to quickly get them working in your website and make your experience smooth.


So far, there are two scenarios I had been through since Episerver introduced continous release process

### Scenario 1 - Released feature


`Serializable Cart` feature has been introduced since **10.2.0**. I won't cover this feature here, you can check out the links in the **Reference** section to get more details. 

By default it is enabled for a new installation and disabled for an upgraded site. 

To enable this feature within your site, you have two options 

#### Option 1 - Configuration

Add the following to `ecf.app.config` file (**CMS solution, not CommerceManager**)

```xml
<Features>
  <add feature="SerializedCarts" state="Enabled" type="Mediachase.Commerce.Core.Features.SerializedCarts,Mediachase.Commerce" />
</Features>
```
#### Option 2 - By code

Add the following to your `InitializeModule` class

```c#
ServiceLocator.Current.GetInstance<IFeatureSwitch>().EnableFeature(SerializedCarts.FeatureSerializedCarts);
```

### Scenario 2 - Beta feature

`CSR UI (Customer Service UI)` feature is a beta feature at the point of time of writing.

By default, all beta features are hidden to prevent unintentional use. To work with Beta features, you need a role defined with the name `EPiBetaUsers`


To enable this beta feature within your site, you first need to add the following to following to `ecf.app.config` file (**CMS solution, not CommerceManager**)

```xml
  <Features>
    <add feature="CustomerServiceUI" state="Enabled" type="EPiServer.Commerce.UI.CustomerService.Features.CustomerServiceUI, EPiServer.Commerce.UI.CustomerService" />
  </Features>
  ```

Secondly, you can either by adding a virtual roles in the virtual role section of the configuration or by creating a role in admin view. Then you add the users to this role. (**NOTE**: Added users to new role, you must log out and in again to see the Beta feature)


```xml
<episerver.framework>
    <appData basePath="App_Data" />
    <scanAssembly forceBinFolderScan="true" />
    <virtualRoles addClaims="true">
      <providers>
        <!-- other roles -->
        <add name="EPiBetaUsers" type="EPiServer.Security.MappedRole, EPiServer.Framework" roles="WebAdmins, Administrators" mode="Any" />
      </providers>
    </virtualRoles>   
  </episerver.framework>
```

![_config.yml]({{ site.baseurl }}/images/episerver-beta-features/beta_feature_1.jpg)
Adding a virtual roles


![_config.yml]({{ site.baseurl }}/images/episerver-beta-features/beta_feature_2.jpg)

Creating a role in admin view

## Reference

[Beta features](https://world.episerver.com/documentation/Items/Installation-Instructions/beta-features/)

[Feature switch](https://world.episerver.com/documentation/developer-guides/commerce/configuration/feature-switch2/)

[Benchmarking Episerver serializable carts](https://world.episerver.com/blogs/andreas-j/dates/2017/6/benchmarking-episerver-serializable-carts2/)


[Introducing SerializableCart mode](https://world.episerver.com/blogs/Son-Do/Dates/2017/1/introduce-serializablecart-mode/)


Happy Coding! 😇