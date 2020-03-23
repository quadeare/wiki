---
title: Drone-ci snippets
description: 
published: true
date: 2020-03-23T13:37:11.718Z
tags: 
---

# Drone-CI

## .drone.yml example

```yml
---
kind: pipeline
type: docker
name: default

steps:
  - name: build
    image: node:8.16.0
    commands:
      - npm ci
      - npm run build
    when:
      branch:
        - master
        - develop

  - name: docker  
    image: plugins/docker
    settings:
      repo: quadeare/resume
      username:
        from_secret: docker_username
      password:
        from_secret: docker_password
      tags: ${DRONE_BRANCH}
```