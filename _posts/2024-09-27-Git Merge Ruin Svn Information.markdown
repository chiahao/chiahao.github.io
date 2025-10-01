---
layout: post
title: "Git Merge Ruin Svn Information"
date: 2024-09-27 15:03:00
category: git
tags: [java]
---

I've successfully used `git svn` to fetch a project from a very old svn server.  
The output of `git svn info` shows:  
- `master` points to `https://svn-server/repos/myProject`.  
- `feature-new` points to `https://svn-server/repos/branches/myProject`.  

However, merging `feature-new` into `master` changes the mapping, causing  
`master` to point to `https://svn-server/repos/myProject/myProject/myBranch`.  

How can I fix this?


SVN repository: 
1. trunk: https://svn-server/repos/myProject
2. branch: https://svn-server/repos/branches/myProject

Procedures for fetching:  
### 1. Clone from svn
```bash
git svn init https://svn-server/repos --trunk=myProject --branches=branches/{myProject} myProject
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
        url = https://svn-server/repos/myProject
        fetch = myProject:refs/remotes/git-svn/trunk
        branches = branches/{myProject}/*:refs/remotes/feature-new/*
[svn]
        authorsfile = ~/authors.txt
```

4. fetch

```shell
git svn fetch
```

5. confirm the remote branches:  

```shell
git branch -r
```

results:  

```shell
feature-new/myProject
git-svn/trunk
```

6. checkout `feature-new/myProject` and rename:  

```bash
git checkout feature-new/myProject
git switch -c feature-new
```



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

