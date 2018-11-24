---
layout: post
title: How do debug CQ/AEM from Intellij 14.x
tags:
  - intellij 14
  - adobe cq
comments: true
---

![_config.yml]({{ site.baseurl }}/images/intellij.png)

## Set up a Web Facet in the Project
1. Go to File -> Project Structure
2. Select the “content” module (the folder contains components,templates)
3. Click “+” above the list of modules and select “Web”
4. As the Web Resource Directory, select the content/src/main/content/jcr_root subdirectory of your project as shown in the screen shot below.

## Set up Debugger

1. Goto Intellij -> Run -> Edit Configurations -> + (Add New Configuration) -> JSR 45 Compatible Server -> Remote
2. Give the debugger a name CQ, remove any Before Launch steps (as we are not really building anything)
3. Add Application server Generic, any start page say Geometrixx English and leave everything default
4. Click on tab Startup/Connection, Debug. Change the port number or leave it default (in the below pic it was changed to 8000)
    ![_config.yml]({{ site.baseurl }}/images/intellij-debugcq/snip20150720_14.png)
5. Restart the CQ instance with the following parameters
    ```java
java -Xdebug -Xrunjdwp:transport=dt_socket,address=8000,suspend=n,server=y -XX:MaxPermSize=512m -Xmx1024M -jar cq-author-4502.jar -nofork    
    ```
6. Click “Debug” icon to start the debugger from Intellij
    ![_config.yml]({{ site.baseurl }}/images/intellij-debugcq/snip20150720_16.png)


Happy Coding! 😇