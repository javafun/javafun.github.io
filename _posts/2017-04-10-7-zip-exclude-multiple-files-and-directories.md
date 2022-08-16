---
layout: post
title: 7 Zip exclude multiple files and directories
tags:  
  - 7zip
comments: true
---

![_config.yml]({{ site.baseurl }}/images/7zip.png)
<!--more-->
## Argument list

* a – Add to archive

* t7z – type of archive, in this example, it uses 7z

* xr@ – specify the exclusion list.

## Examples

Adds to the archive.7z all files from Folder1 and its subfolders, except *.png files.

```
7z a archive.7z Folder1\ -xr!*.png

```

To exclude the list of directories and files, you can first store the items in a text file separated by new line for each, then run the following command

```
7z.exe a -t7z archive.7z C:\Project\Solution1 -xr@exclusionList.txt
```

Happy Coding! 😇