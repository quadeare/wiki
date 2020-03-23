---
title: Git
description: 
published: true
date: 2020-03-23T14:49:45.613Z
tags: 
---

# Git

## Remote

### Add remote

```bash
git remote add my-new-remote git@github.com:example/example.git
```

### Remove remote

```bash
git remote remove my-new-remote 
```

## Submodules

### Add a submodule

```bash
git submodule add git@github.com:example/example.git ./submodule
```

### Remove a submodule

```bash
git submodule deinit $(SUBMODULE)
git rm ./submodule
```

## Rebase

### Merge multiple commit into one

Example with 3 commits :

```bash
5d2d46ca9bfcf48385aa8021020683742782e22c d
af6c0deca9c2cedf329801f9a637dcc727b8f739 c
97bd207983f7b3154d8c2dc23a7f5f5b146421a0 b
35b99d1de62293f78e35b7c04f4067e5737b018d a
```

Merging these three commits into one :

```bash
git rebase -i 35b99d1de62293f78e35b7c04f4067e5737b018d
```

Edit the commit :

```bash
pick 97bd207 b
s af6c0de c
s 5d2d46c d
```

And after :

```bash
070ed2d (HEAD -> master) b
35b99d1 a
```




