---
layout: post
title: "git-svn From GitHub To Svn"
date: 2024-03-30 12:11:00
category: programming
tags: [git-svn]
---


### 1. Clone from svn
```bash
git svn init https://140.122.66.77/svn/personnel_matters --trunk=PrivLib --branches=MavenizeProjects/{PrivLib} PrivLib
```

### 2. Setting the authorsfile

```bash
git config svn.authorsfile ~/authors.txt
```

3. Edit content of `.git/config`:    

```bash
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false  
        logallrefupdates = true
        ignorecase = true
        precomposeunicode = true
[svn-remote "svn"]
        url = https://140.122.66.77/svn/personnel_matters
        fetch = PrivLib:refs/remotes/origin/trunk
        branches = MavenizeProjects/{PrivLib}/*:refs/remotes/origin/*
[svn]
        authorsfile = ~/authors_PmbMgr.txt
```

Modify these line:  
```xml
fetch = PrivLib:refs/remotes/origin/trunk
branches = MavenizeProjects/{PrivLib}/*:refs/remotes/origin/*
```  

to

```xml
fetch = PrivLib:refs/remotes/git-svn/trunk
branches = MavenizeProjects/{PrivLib}:refs/remotes/feature-jdk17/*
```

4. fetch

```shell
git svn fetch
```

5. checkout `feature-jdk17/PrivLib`

```xml
Note: switching to 'feature-jdk17/PrivLib'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 08b92ec jdk17版: 已同步原 jdk6 的 r5161
➜  ~/Downloads/PrivLib git:(08b92ec) git branch
➜  ~/Downloads/PrivLib git:(08b92ec) 
```

6. switch -c

```bash
git switch -c feature-jdk17
```



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

