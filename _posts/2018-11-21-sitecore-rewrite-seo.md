---
layout: post
title: Sitecore seo rewrite rules
tags:
  - sitecore
  - url rewrite

comments: true
---


List of Sitecore SEO / Security rewrite rules I recently added to one of the project. 


## Lower case rule

```xml
<rule name="Lower Case Rule" stopProcessing="true">
  <match url="[A-Z]" ignoreCase="false" />
  <conditions>
    <add input="{REQUEST_METHOD}" matchType="Pattern" pattern="POST" ignoreCase="true" negate="true" />
    <add input="{URL}" pattern="^.*\.(axd|css|js|jpg|jpeg|png|gif|txt|xml|svg|pdf)$" negate="true" ignoreCase="true" />
  </conditions>
  <action type="Redirect" url="{ToLower:{URL}}" />
</rule>
<rule name="HTTP to HTTPS redirect" stopProcessing="true">
  <match url="(.*)" />
  <conditions>
    <add input="{HTTPS}" pattern="off" ignoreCase="true" />
  </conditions>
  <action type="Redirect" url="https://{HTTP_HOST}/{R:1}"
      redirectType="Permanent" />
</rule>
```

## Remove server header rule
```xml
<rule name="Removing server header" enabled="true">
  <match serverVariable="RESPONSE_SERVER" pattern=".*" />
  <action type="Rewrite" value="MyServer" replace="true" />
</rule>
```

### Add strict transport security 

```xml
<rule name="Add Strict-Transport-Security when HTTPS" enabled="true">
  <match serverVariable="RESPONSE_Strict_Transport_Security"
      pattern=".*" />
  <conditions>
    <add input="{HTTPS}" pattern="on" ignoreCase="true" />
  </conditions>
  <action type="Rewrite" value="max-age=31536000" />
</rule>
```