---
layout: post
title: Customize association types for Releated Entities 
tags:
  - episerver
  - episerver commerce
comments: true
---

![_config.yml]({{ site.baseurl }}/images/episerver-new.png)
Customizing Related Entities association type does't seem to be covered very well in Episerver documentation. In this post, I'll quickly show you how easily this can be achieved. 


## Define custom types for Related Entities

1. Create a new `InitializationModule` class.
2. Use Episerver `ServiceLocator` to create an instace of `AssociationGroupDefinition`.
3. Add your custom association type via `Add` method. (**Note:** `Add` method perofrms type name existence check, therefore you won't accidentally add duplicate type.)
![_config.yml]({{ site.baseurl }}/images/episerver-customize-association-types/img3.jpg)
4. Build solution, log in to CMS and navigate to Product's Related Entities, you'll see other types than the out-of-the-box Default type.
![_config.yml]({{ site.baseurl }}/images/episerver-customize-association-types/img2.jpg)



```c#
[InitializableModule]
[ModuleDependency(typeof(EPiServer.Web.InitializationModule))]
public class AssociationTypeInitialization : IInitializableModule
{
    public void Initialize(InitializationEngine context)
    {
        var associationTypeRepository = context.Locate.Advanced.GetInstance<GroupDefinitionRepository<AssociationGroupDefinition>>();

        associationTypeRepository.Add(new AssociationGroupDefinition() { Name = "cross-selling" });
        associationTypeRepository.Add(new AssociationGroupDefinition() { Name = "upselling" });
    }

    public void Uninitialize(InitializationEngine context){}
}
```
## Querying association types 

Association types are stored in `tblBigTable` under the hood. You can use the query below to verify how many types defined in the system.

```sql
SELECT TOP 10 * 
FROM   tblBigTable 
WHERE  storename = 
       'EPiServer.Commerce.Catalog.Linking.AssociationGroupDefinition' 
```


Happy Coding! 😇
