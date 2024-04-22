---
layout: post
title: How to synchronize data between Omron connect app and Apple Health 
tags:
  - omron
  - HEM-7600T
  - Blood pressure monitor
comments: true
image:
  path: /images/HEM-7600T-1.jpg
---

Recentlly, I upgraded my blood pressure monitor from old mode [HEM-7121](https://www.mobileciti.com.au/omron-hem7121-standard-blood-pressure-monitor-white?utm_term=&hsa_mt=&hsa_kw=&gad_source=1){:target="\_blank"} to [HEM-7600T](https://www.chemistwarehouse.com.au/buy/84602/omron-smart-elite-hem7600t-blood-pressure-monitor-bluetooth-tubeless){:target="\_blank"}. This is a great machine and I'm extremely happy with this upgrade, however I did encounter data synchronization issue from omron to Apple Health and I could not find a clear solution from internet, ChatGPT could not help either in this instance as well. 

<!--more-->
I have gone through the manual, unfortunately the manual seems a bit out of date, and confused as it states data sync is only supported in US,CAN and EMEA. I contacted the support through the app, luickly I got solution from their support.  

## Solution 

Once you installed the app and registered your device, follow the steps below

1. Select `contents` option from the bottom bar on the Omron Connect App, you will then  see the option to `add contents` button
   <img src="images/hem-7600/step1.png" width="20%"/>
2. Click on `add contents` button and scroll to the bottom
   <img src="images/hem-7600/step2.png" width="20%"/>
3. You'll see the `Apple Health Data Sharing` section at the bottom and click on `Share setting` button
    <img src="images/hem-7600/step3.png" width="20%"/>
4. Turn on the data sync and you're ready to go.
 <img src="images/hem-7600/step4.png" width="20%"/>

> Once you have begun sharing you will need to wait for a short time for the syncing to come through.
{: .prompt-tip }


I hope this clears out how to sync data from Omron connect App to Apple Health. I would suggest you contact their support directly using the app in case if this does not work for you. Their support service is very resposive and superior. Thanks Omron support team :)

