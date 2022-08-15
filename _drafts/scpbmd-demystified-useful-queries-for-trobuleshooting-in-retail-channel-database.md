---
layout: post
title: SCpbMD demystified - Useful queries for trobuleshooting in CDB (Retail Channel Database)
tags:  
  - sitecore
  - dynamics ax 2012r3 (CU9) 
  - sitecore commerce
  - sitecore commerce connect
comments: true
---

![_config.yml]({{ site.baseurl }}/images/scpbmd.png)


## Order & Order details 

#### Order header query
```sql

select * from ax.RETAILTRANSACTIONTABLE

```

#### Order details query
```sql

select * from ax.RETAILTRANSACTIONSALESTRANS

```

## Customer & Account

#### Customer view

```sql

select * from crt.CUSTOMERSVIEW

```

#### Customer activation query

When triggering an email, Dynamics AX will generate activation code and store in `crt.RETAILCUSTOMEREMAILACTIVATION` table and its usage. 

```sql

select * from crt.RETAILCUSTOMEREMAILACTIVATION where EMAIL = '<email>'

```



Happy Coding! 😇