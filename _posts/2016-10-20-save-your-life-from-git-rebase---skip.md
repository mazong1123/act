---
layout: post
title: Save your life from git rebase --skip
date: 2016-10-20 23:43
author: mazong1123
comments: true
categories: [Uncategorized]
published: true
---
Changes could be lost if we execute git rebase --skip. Following are steps to rescue
your changes:

1. Backup .git folder.
2. Go to .git/logs/refs/heads, find the file with the branch name you are working on.
3. Open that file, you'll see something like this:

```
0000000000000000000000000000000000000000 ebba9357da9fe2c0961e70916f2d17fd93888f64 mazong1123 <mazong1123@gmail.com> 1476774555 +0800	clone: from http://xxx
f229808a504b46406f043f31388fdb905592cb45 e23231b8230dad219e04147fb4b06a4ff9033164 mazong1123 <mazong1123@gmail.com> 1476882915 +0800	commit: Renamed xxx to yyy.
e23231b8230dad219e04147fb4b06a4ff9033164 48a3d23985b6b97cbaecd84e60861c0175371d72 mazong1123 <mazong1123@gmail.com> 1476884266 +0800	rebase finished: refs/heads/develop onto 48a3d23985b6b97cbaecd84e60861c0175371d72

```

4. Let's say we want to rescue the changes on commit "Renamed xxx to yyy". We should remember the second hash value

```
e23231b8230dad219e04147fb4b06a4ff9033164
```

5. Execute following command. And the changes are back!

```
git checkout -b recovery_branch e23231b8230dad219e04147fb4b06a4ff9033164
```
