---
layout: post
title: Unable to launch the IIS Express Web server...
tags:
  - iisexpress
  - visual studio 2022  
comments: true
image:
  path: /images/iisexpress/vs_iisexpress.png
---
Nowadays, I don't quite often use IIS express web server for web development since I move to .NET core and Kestrel becomes my favourite local development server. However, when I need to support legacy customers solution, I prefer choose IIS express first before moving to IIS server. I barely have issue with IIS express except this annoying one randomly happened and it always takes me decent amount of time to get everything working again. 


<!--more-->
In this blog post, I decide to document one of the root cause for this issue I encountered and the fix, so I don't have to spend more than a few minutes whenever I encounter this issue again. 

## Symptom

```
---------------------------
Microsoft Visual Studio
---------------------------
Unable to launch the IIS Express Web server.

Failed to register URL "http://localhost:xxxx/" for site "xxxxxx" application
"/". Error description: The process cannot access the file because it is being
used by another process. (0x80070020)

---------------------------
OK   
---------------------------
```

## Causes
According to my research, it looks like many ports are restricted/reserved to access on Windows machines on some Windows updates or applications

You can use the following command to list the reserved ranges.

```bat
netsh interface ipv4 show excludedportrange protocol=tcp
```

If you find the port configured in Visual Studio listed in above command, it means the port is not available for use by IIS express. 

## Fixes

The fix would be much easier once the root cause has been identified. 

There are two solutions and both of them works fine me. 

### Solution 1

Change to different port that are not in the reserved ranges

### Solution 2

Run the following command

1. Stop `winnat`
```bat
net stop winnat
```
2. Start your web application
3. Start `winnat`
```bat
net start winnat
```
I hope you find this blog post helpul and get your development environment back to normal quicker. 

## References
* ["Unable to launch the IIS Express Web server." in Visual Studio](https://stackoverflow.com/questions/29116292/unable-to-launch-the-iis-express-web-server-in-visual-studio){:target="_blank"}
* [Visual studio 2019 “Unable to connect to web server 'IIS Express'”](https://stackoverflow.com/questions/68694790/visual-studio-2019-unable-to-connect-to-web-server-iis-express){:target="_blank"}
* [Unable to start Kestrel getting 'An attempt was made to access a socket in a way forbidden by its access permissions'](https://superuser.com/questions/1486417/unable-to-start-kestrel-getting-an-attempt-was-made-to-access-a-socket-in-a-way){:target="_blank"}
* [Many excludedportranges how to delete - hyper-v is disabled](https://superuser.com/questions/1579346/many-excludedportranges-how-to-delete-hyper-v-is-disabled/1610009){:target="_blank"}

Happy Coding! 😇
