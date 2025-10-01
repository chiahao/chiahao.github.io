---
layout: post
title: "Git Checkout Remote Branch"
date: 2022-10-17 10:40:00
category: programming
tags: [git]
---

```bash
git checkout -b Lesson4 origin/Lesson4
```

如果只是單純 `checkout`:  

```bash
git checkout origin/Lesson4
```

就會產生以下警告:  

```bash
Note: checking out 'origin/Lesson3'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at 02c93f5 Lesson 3: MVVM and the Swift type system
```

查看 [【冷知識】斷頭（detached HEAD）是怎麼一回事？](https://gitbook.tw/chapters/faq/detached-head):  

1. 使用 Checkout 指令直接跳到某個 Commit，而那個 Commit 剛好目前沒有分支指著它。
2. Rebase 的過程其實也是處於不斷的 detached HEAD 狀態。
3. 切換到某個遠端分支的時候。

> 這有什麼影響嗎？影響就是當我的 HEAD 回到其它分支之後，這個 Commit 就不容易被找到（除非你有記下這個 Commit 的 SHA-1 值），
> 如果一直沒人來找它，過久了之後就會被 Git 啟動的資源回收機制給收掉了。

如果還想留下這個 Commit，就給它一個分支指著它就行了。如果你剛好就在這個 Commit 上的話：

```bash
$ git branch tiger
```

或是明確的跟 Git 說幫你建立一個分支指向某個 Commit：

```bash
$ git branch tiger 02c93f5
```

> 也可以使用 Checkout 指令配合 -b 參數，建立分支後直接切換：

```bash
$ git checkout -b tiger 02c93f5
```

### 為什麼切換到遠端的分支也會是這個狀態？
> 更正確的說，應該是說「當 HEAD 沒有指到某個『本地』的分支」就會呈現這個狀態。

> 要切換到遠端分支而不呈現 detached HEAD 狀態，可以加上 `--track` 或 `-t` 參數：
> `-t` 參數是指會在本機建立一個名為追蹤分支（tracking branch）的東西。



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


