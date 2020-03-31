---
title: Some Docker tips and tricks
description: 
published: true
date: 2020-03-31T13:59:21.748Z
tags: 
---

# Docker tips and tricks

## Installation

### One shot install 

```bash
curl -fsSL https://get.docker.com | sh
```

## Some usefull commands

### Remove all untagged images

```bash
docker rmi $(docker images | grep '^<none>' | awk '{print $3}')
```

