---
layout: post
title: Create a read-only user in Azure SQL
tags:  
  - azure  
comments: true
---

![_config.yml]({{ site.baseurl }}/images/azure-sql.jpg ){:width="50%"}
One of my colleagues asked me how to create a read-only user for a particular database in Azure SQL, I thought it would be similar process as how I did in SQL server. As it turned out, it wasn't really straightforward. I decide to share my learning in this blog post.  
<!--more-->

## Step 1

Run the following scripts to create user (1st script) and grant db (2nd script)

```sql

CREATE USER [yourusername] WITH PASSWORD = 'strong password';

```

```sql
ALTER ROLE [db_datareader] ADD MEMBER [yourusername];
```

## Step 2

Open your SQL Management Studio (SSMS). Fill the login details with the username/password created above, click on **Options** and enter the database name. 

<img src="/images/azure-sql/1.png" width="700" style="display:block"/>
<img src="/images/azure-sql/2.png" width="700" style="display:block"/>

> NOTES: You must always specify the database name as the user created with step 1 SQL script is using [Contained Database User Model](https://docs.microsoft.com/en-us/sql/relational-databases/security/contained-database-users-making-your-database-portable?view=sql-server-ver15)




## References
* [Contained Database Users - Making Your Database Portable](https://docs.microsoft.com/en-us/sql/relational-databases/security/contained-database-users-making-your-database-portable?view=sql-server-ver15)
* [Database-Level Roles](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/database-level-roles?view=sql-server-ver15)
* [Permissions (Database Engine)](https://docs.microsoft.com/en-us/sql/relational-databases/security/permissions-database-engine?view=sql-server-ver15)

Happy Coding! 😇