---
layout: post
title: Mongo DB Shell Command – Create Database
tags:
  - mongodb
comments: true
---

![_config.yml]({{ site.baseurl }}/images/mongodb.png)


1. Connect to shell by running **mongo**
2. To create a database, enter **Use**  command in the shell. (The command will create a new database, if it doesn’t exist, otherwise it will return the existing database)
3. You need to insert at least one document to make it display in the db list command. Enter **db..insert({name:"test"})**command to create the first document.

## Reference

[http://www.tutorialspoint.com/mongodb/mongodb_create_database.htm](http://www.tutorialspoint.com/mongodb/mongodb_create_database.htm)

Happy Coding! 😇