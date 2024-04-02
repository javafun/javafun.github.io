---
layout: post
title: Jenkins 2.0 Set Up on OSX
tags:
  - jenkins
comments: true
image:
  path: /images/jenkins.png
---

<!-- ![_config.yml]({{ site.baseurl }}/images/jenkins.png) -->
<!--more-->

## Prerequisite

- JAVA JDK 7 or above
- GIT
- MAVEN 3 or above

## Install Jenkins

- Install jenkins via homebrew
- brew update &amp;&amp; brew install jenkins

## Starting Jenkins

After Jenkins is installed successfully, follow the instructions to start Jenkins on login

```bash
ln -sfv /usr/local/opt/jenkins/*.plist ~/Library/LaunchAgents
```

If you want to configure Jenkins to launch on system startup, for all users on OS X, then copy the plist file to the system Launchd location instead

```bash

sudo cp -fv /usr/local/opt/jenkins/*.plist /Library/LaunchDaemons

sudo chown `whoami` /Library/LaunchDaemons/homebrew.mxcl.jenkins.plist

```

You can always start Jenkins manually with

```bash
/usr/local/bin/jenkins
```

or if you have set up your PATH correctly when installing Homebrew, simply

```bash
jenkins
```

## Starting Jenkins as service

#### Start service

```
brew services start jenkins
```

#### Stop service

```
brew services stop jenkins
```

#### Restart service

```
brew services restart jenkins
```

## Restarting Jenkins

If you have an older version of Jenkins and you are upgrading it, then you can restart it this way:

```bash
launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist

launchctl load ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist
```

## Install Jenkins Plugins

- Git
- Maven
- Parameterized Trigger Plugin (This plugin will simplify the maven profile configuration)
- JUnit
- PMD / FindBugs / Checkstyle (For quality analysis)
- Greenball

## Configure Jenkins

Go to Manage Jenkins -&gt; Global Tool Configuration, configure the following sections

#### JDK

- Deselect Intall automatically as we will use the installed JDK
- Fill the JDK Name E.g. JDK 1.7
- Specify the JAVA_HOME path. E.g. /Library/Java/JavaVirtualMachines/jdk1.7.0_79.jdk/Contents/Home

#### Maven

- Deselect Intall automatically as we will use the installed Maven
- Fill the Maven Name E.g. Maven 3
- Specify the MAVEN_HOME path. E.g. /usr/local/opt/maven31/libexec

#### Git

Git intallation should be picked up by default, unless you install GIT after Jekins.

## Set Up Job

1. Create new maven project by giving a new.
2. Go to Source Code Management sections, add repositories link.
3. If you want to use SSH, click Add button in Credentials section. In the dialog, choose SSH Username with private key option, then select From the jenkins master ./ssh, Note: Dont put any value into Username
4. Click Build Now to test the job.

## Uninstall Jenkins

Execute uninstall script from terminal:

```bash
/Library/Application Support/Jenkins/Uninstall.command
```

## Reference

[Homebrew](http://brew.sh/)

[Installing Jenkins OS X Homebrew](http://flummox-engineering.blogspot.com/2016/01/installing-jenkins-os-x-homebrew.html)

[Maven doesn’t have a ‘lib’ subdirectory in Jenkins](http://flummox-engineering.blogspot.com/2016/01/maven-doesnt-have-a-lib-subdirectory-jenkins.html)

_Solution:_

> The ‘lib’ folder should be linking to libexec subdirectory.
> If you install your maven via homebrew, your maven home should /usr/local/opt/maven31/libexec. (Note: maven31 is the version I installed on my mac, change this according to your local setting.)

[Jenkins CI on OSX](https://gist.github.com/ostinelli/972cfdb4bce51d428d3b)

Happy Coding! 😇
