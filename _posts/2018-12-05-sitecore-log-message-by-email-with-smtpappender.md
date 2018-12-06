---
layout: post
title: Sitecore Log Message by Email With SmtpAppender (Sitecore 8.2)
tags:
  - sitecore
  - log4net
  - smptappender
comments: true
---

![_config.yml]({{ site.baseurl }}/images/sitecore.png)
Recently, I was trying to enable to log the fatal errors by email using Sitecore log framework. 



I thought this would be a simple task that only requires a few configuration changes as I remembered that `Sitecore.Logging` use log4net by default and I have been used `log4net` for many years, I am very confident with log4net configuration. It turns out it is not, absolutely not. 

I spent a few hours trying to figure out why the same configuration works in my test console application but not in Sitecore. Interestingly, after decompile `Sitecore.Logging dll`, I found out although `Sitecore.Logging` uses the same namespace as log4net and works similar to it, Sitecore.Logging has no dependency on log4net, in other words Sitecore has complied log4net source code into its own DLLs.

At the time of writing this blog post, I haven't figured out which log4net version has been used by `Sitecore.Logging` internally, but I found some features in log4net are not available in `Sitecore.Logging`.


## TL;DR

To enable Sitecore log messages via email you need to set up an instance of the SMTPAppender class in `Sitecore.config` or patch in your own config file.

```xml
<appender name="SmtpAppender" type="log4net.Appender.SmtpAppender, Sitecore.Logging">
    <to value="support-team@yourdomain.com"/>
    <from value="no-reply@yourdomain.com"/>
    <subject value="Critical error occured"/>
    <smtpHost value="smtpserver.yourdomain.com"/>
    
    <!-- port is not working -->
    <!-- <port value="25"/> -->
    
    <!-- EnableSsl is not working -->
    <!-- <EnableSsl value="false" /> -->
    <bufferSize value="2"/>
    <threshold value="FATAL"/> 

    <layout type="log4net.Layout.PatternLayout">
      <conversionPattern value="%4t %d{ABSOLUTE} %-5p %m%n"/>
    </layout>
</appender>

```

There are a few important element(s) and attribute(s) you need to get it right in order to trigger the email

* **type** attribute - the class name uses log4net default namespace i.e `log4net.Appender.SmtpAppender`, but the assembly name must be `Sitecore.Logging`
* **port** and **EnableSsl** elements - these elements are not supported in the Sitecore version I used (Sitecore 8.2 update 6).
* **threshold** - I used `<level>` in log4net configuration throughout other projects, however it doesn't work in the sitecore, switch over to `<threshold>`, everything works fine.


The `SmtpAppender` defined above uses the following [Conversion pattern name](https://logging.apache.org/log4net/log4net-1.2.13/release/sdk/log4net.Layout.PatternLayout.html){:target="_blank"} to format the log event as a string.
```
%d = Date
%n = New Line
%m = The message
%4t = Thread Id
%-5p = Logging Level
```

## Full patch config example

```xml
 <sitecore>
    <log4net>
      <appender name="SmtpAppender" type="log4net.Appender.SmtpAppender, Sitecore.Logging">
          <to value="support-team@yourdomain.com"/>
          <from value="no-reply@yourdomain.com"/>
          <subject value="Critical error occured"/>
          <smtpHost value="smtpserver.yourdomain.com"/>
          
          <!-- port is not working -->
          <!-- <port value="25"/> -->
          
          <!-- EnableSsl is not working -->
          <!-- <EnableSsl value="false" /> -->
          <bufferSize value="2"/>
          <threshold value="FATAL"/> 

          <layout type="log4net.Layout.PatternLayout">
            <conversionPattern value="%4t %d{ABSOLUTE} %-5p %m%n"/>
          </layout>
      </appender>
      <root>
        <appender-ref ref="SmtpAppender"/>
      </root>
    </log4net>    
  </sitecore>
```

## References

[Log4net Pattern Layout](https://logging.apache.org/log4net/log4net-1.2.13/release/sdk/log4net.Layout.PatternLayout.html)




Happy Coding! 😇