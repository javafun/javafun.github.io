---
layout: post
title: MacOS brew upgrade failure - undefined method uses_from_macos for Formulary
tags:
  - OSX
comments: true
---

![_config.yml]({{ site.baseurl }}/images/osx.jpg)
Today when I upgrade my outdated packages with Homebrew and encounter this nasty error. 


## Symptom
```
Error: glib: undefined method `uses_from_macos' for Formulary::FormulaNamespace1b33d7b036781a8c4dc38a980a07e0d5::Glib:Class
```

## Causes
Run `brew --version`, the console shows my Home4rew version is 2.1.4 which is out of dated. 

## Fixes
Run the command below to update Homebrew to latest version 2.1.6, then run upgrade again.
`cd "$(brew --repo)" && git fetch && git reset --hard origin/master && brew update`



Happy Coding! 😇
