---
layout: post
title: Drupal WebForm module
tags:
  - drupal
  - webform
comments: true
image:
  path: /images/drupal.png
---

<!-- ![_config.yml]({{ site.baseurl }}/images/drupal.png) -->
<!--more-->

## Installation

Drush

```
Drush dl WebForm
```

## Customization

- Hook API
- Theme

## Advanced feature

- Build-in Fieldset
  - Group a set of form fields
- PageBreak
  - Split complex form into multiple steps like wizards

## Token

#### Webform email template hidden tokens

You reference to the php server variables with drupal token by using %server[variable name]

e.g. To reference the domain url from email template, you can use %server[SERVER_NAME]

## Documentation

http://drupal.org/documentation/modules/webform

## Resources

Module download link - http://drupal.org/project/webform

Video Tutorial - http://drupal.org/node/1351064

Happy Coding! 😇
