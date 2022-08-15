---
layout: post
title: Sitecore – Add missing icons for specific media types
tags:  
  - sitecore
comments: true
---

![_config.yml]({{ site.baseurl }}/images/sitecore.png)
Recently, I was trying to save the PDF file in the media library and found this issue. The PDF file used empty icon instead.

Luckily, this seems a common issue and solution can be easily googling out. Sitecore has official document in its knowledge base about this issue.

[Missing icons for specific media types](https://kb.sitecore.net/articles/469199)

What I want to point out is if you search this issue from google, you will be very likely found some other blog posts provide the similar approach, the only difference comparing to Sitecore official document is the type specified in the generator.

```
<generator type="Sitecore.Resources.Media.MediaThumbnailGenerator, Sitecore.Kernel">
```

The type seems redundant or causing icon failed to be displayed in my current Sitecore v8.0 update 3.

Below is my patch config instead of modifying the web.config

```xml
<mediaLibrary>
  <mediaTypes>
    <mediaType name="PDF file" extensions="pdf" patch:before="*[@name='AVI video']" >
    <mimeType>application/pdf</mimeType>
      <forceDownload>false</forceDownload>
      <sharedTemplate>system/media/unversioned/pdf</sharedTemplate>
      <versionedTemplate>system/media/versioned/pdf</versionedTemplate>
      <thumbnails>
        <staticFile>/sitecore/shell/Themes/standard/images/pdf_icon.png</staticFile>
      </thumbnails>
    </mediaType>
  </mediaTypes>
</mediaLibrary>

```

Happy Coding! 😇