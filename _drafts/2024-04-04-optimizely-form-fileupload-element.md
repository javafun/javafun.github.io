---
layout: post
title: Optimizely Form - Fileupload Gotcha
tags:
  - optimizely
  - optimizely cms
  - optimizely cms 12
comments: true
image:
  path: /images/optimizely_cms.png
---

Optimizely form has built-in fileupload element enabling marketers to effortlessly create forms with file upload capabilities. However, there are a few potential pitfalls associated with this form element that developers must ensure are configured correctly.
<!--more-->

This form element has a few configurations allow to manage file size and types a visitor can upload, and I highliy recommend you review these settings and apply proper values.


![alt text](images/optimizelyform-fileupload/fileupload_config.png){: w="500" h="500"}


> In order to get form submitted correctly along with uploaded file(s), your solution **MUST** have at least one [media type](https://docs.developers.optimizely.com/content-management-system/docs/media-types-and-templates){:target="_blank"} defines a list of file extensions and the allowed extensions you specified in the fileupload element **MUST** exist in the media type file extenion list.
{: .prompt-tip }

The following code snipet is an example of media type definition.

```csharp
[ContentType(DisplayName = "FormUploadFile", GUID = "7BD7FA9F-F1B5-42D8-B4CA-444426E162CB", Description = "")]
[MediaDescriptor(ExtensionString = "pdf,doc,docx,txt")]
public class FormUploadFile : MediaData
{

}
```


## Reference

* [Form element types](https://support.optimizely.com/hc/en-us/articles/4413192345101-Form-element-types){:target="_blank"}
* [Configure Optimizely Form](https://docs.developers.optimizely.com/content-management-system/v1.2.0-forms/docs/configuring-optimizely-forms){:target="_blank"}
* [Media types and templates](https://docs.developers.optimizely.com/content-management-system/docs/media-types-and-templates){:target="_blank"}

Happy Coding! 😇
