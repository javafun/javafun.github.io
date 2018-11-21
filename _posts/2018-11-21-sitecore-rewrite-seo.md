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

<script src="https://gist.github.com/javafun/751f2afea4dedf05b065f1cbadb37bfb.js"></script>

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
