---
layout: post
title: LocalDb - Logon failed for login 'xx\xxx' due to trigger execution
tags:
  - LocalDb
comments: true
image:
  path: /images/localdb-logonfailed/IHXCB.jpg
---

<!-- ![_config.yml]({{ site.baseurl }}/images/localdb-logonfailed/IHXCB.jpg) -->

I encountered an issue - `Logon failed for login 'xx\xxx' due to trigger execution` today when I tested my local site. I expanded details from SSMS to investigate with no luck. I tried to re-install SQL 2019 localdb, reverted back to old version of localdb, none of them fixed my issue.

<!--more-->

<img src="/images/localdb-logonfailed/PWVB2.jpg" width="700" style="display:block"/>

## Fixes

After spending nearly an hour on this issue, I concluded my localdb `MSSQLLocaldb` was corrupted. I decided to delete and re-create `MSSQLLocaldb` to see if it works. Luckily, this approach fixed my issue.

### Step 1 - Delete `MSSQLLocaldb` folder

The folder can be found from the location below.

```
C:\Users\<username>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances
```

### Step 2 - Re-create `MSSQLLocaldb` database

Run the following command from your terminal

```
sqllocaldb create MSSQLLocaldb

```

## References

[Logon failed for login due to trigger execute](https://dba.stackexchange.com/questions/218811/logon-failed-for-login-due-to-trigger-execution)

Happy Coding! 😇
