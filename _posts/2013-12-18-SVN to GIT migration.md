---
layout: post
title: SVN to GIT migration
tags:
  - svn
  - git
comments: true
---

![_config.yml]({{ site.baseurl }}/images/git.jpg)
<!--more-->
The following script will automate svn to git migration. Save this in your svn directory `svn2git.sh`

<script src="https://gist.github.com/javafun/abab170e33e39b3c54715283e0dbacc9.js"></script>

1. Clone the svn repository with “git svn” command
    e.g. `git svn clone [SVNProjectRootDirectory] -T [TrunkDirectoryName] -b [BranchDirectoryName] -t [TagDirectoryName]`
2. Loop through all the remote branches/tags and check them out to local respectively.
3. Push all local branches/tags to the new repository.

USAGE:

```
svn2git.sh [GitRepositoryUrl]  [SvnRepositoryUrl]   [TrunkDirectoryName]   [BranchDirectoryName]   [TagDirectoryName]
```


Happy Coding! 😇