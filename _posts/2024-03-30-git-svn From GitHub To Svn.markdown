---
layout: post
title: "git-svn From GitHub To Svn"
date: 2024-03-30 12:11:00
category: programming
tags: [git-svn]
---

#### [Updating a git mirror of an SVN repository](https://stackoverflow.com/questions/10886784/updating-a-git-mirror-of-an-svn-repository)


[Reviving a git-svn clone](https://rip747.wordpress.com/2009/06/17/reviving-a-git-svn-clone/)

### 1. Clone from GitHub  
```bash
git clone [github url]
cd repo
```

### 2. Check Ref  

```bash
git branch -r   
```
e.g.   

```bash
  origin/HEAD -> origin/feature-jdk17
  origin/feature-jdk17  
  origin/master  
```

Content of `.git/config`:    
```bash
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
[remote "origin"]
        url = https://github.com/chiahao/MyProj.git
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
        remote = origin
        merge = refs/heads/master
```


### 3. Relate to Svn

```bash
git svn init [svn url]  
```

will add  some content to `.git/config`:    

```bash  
...  
[svn-remote "svn"]
        url = https://svn-server/MyProj
        fetch = :refs/remotes/git-svn   
```

### 4. Update Ref

```bash
git update-ref refs/remotes/git-svn refs/remotes/origin/[`master` or other branch name]  
git svn rebase
```


> This is the secret sauce! What I’m doing here is updating the HEAD of the git-svn remote  
(refs/remotes/git-svn, this is created for you by doing the "git svn init") to match the HEAD I grabbed from github  
(refs/remotes/origin/[**master**], again this is created for you by doing the "git clone").

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

