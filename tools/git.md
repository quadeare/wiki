---
title: Git
description: 
published: true
date: 2020-03-23T14:41:28.595Z
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



