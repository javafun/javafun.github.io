---
layout: post
title: SCpbMD demystified - AX payment configuration & trobuleshooting
tags:  
  - sitecore
  - dynamics ax 2012r3 (CU9) 
  - sitecore commerce
  - sitecore commerce connect
comments: true
---

![_config.yml]({{ site.baseurl }}/images/scpbmd.png)


### Connector to service request not found \r\n ValidationResults


![_config.yml]({{ site.baseurl }}/images/ax-payments/payment-configuration.png)


Use the query below to figure out available payment connectors from the AX.


```sql
  SELECT * FROM crt.PAYMENTCONNECTORVIEW
```

Happy Coding! 😇