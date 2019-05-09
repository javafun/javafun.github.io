---
layout: post
title: Resolving missing large thumbnail in Commerce Catalog
tags:
  - episerver
  - episerver commerce
comments: true
---

![_config.yml]({{ site.baseurl }}/images/episerver-new.png)
I had this issue back to 3 years ago when I helped client to implement B2C Commerce solution on `Episerver Commerce 9`. I almost forget this until I hit on this issue again while preparing my Episerver Commerce certification exam recently. So I decide to write a quick blog post to share my solution.


## Where is my thumbnail going?
The screenshow below is what you'll see in the Commerce catalog if you start a fresh new Commerce site with default `ImageData` or custom class directly inherited from `ImageData`.
![_config.yml]({{ site.baseurl }}/images/resolve-missing-large-thumbnail/1.jpg)

Luckily, this issue can be resolved easily without much coding involved. There are two options you can use depends on your current solution.

## Option 1 - CommerceImage
If you're in the new solution build, you can simply inherit custom image class from `CommerceImage` instead of `ImageData`. 

```c#
[ContentType(DisplayName = "ImageModel", GUID = "cb418237-9254-4192-b79d-1de0661151bf", Description = "")]
[MediaDescriptor(ExtensionString = "jpg,jpeg,jpe,ico,gif,bmp,png")]
public class ImageModel : CommerceImage
{
    public virtual string ImageDescription { get; set; }

}
```


## Option 2 - LargeThumbnail property

If you have already had custom class that inherited from `ImageData`, you can add `LargeThumbnail` property to your class.

```c#
[ContentType(DisplayName = "ImageModel", GUID = "cb418237-9254-4192-b79d-1de0661151bf", Description = "")]
[MediaDescriptor(ExtensionString = "jpg,jpeg,jpe,ico,gif,bmp,png")]
public class ImageModel : ImageData
{
    [Editable(false)]
    [ImageDescriptor(Width = 256, Height = 256)]      
    public virtual Blob LargeThumbnail { get; set; }

    public virtual string ImageDescription { get; set; }
}
```

Happy Coding! 😇
