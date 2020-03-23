---
title: Gitlab-ci examples
description: 
published: true
date: 2020-03-23T13:34:15.784Z
tags: 
---

# Gitlab-ci

## Gitlab-ci.yml example

```yml
services:
  - docker:dind

image: docker:latest

variables:
  MYGLOBAL_VARIABLE: "payload"

stages:
  - pull

pull:
  stage: pull
  image: alpine/git
  before_script:
  	- mkdir data
  script:
    - git clone <another_git> data/
  artifacts:
    expire_in: 60 minutes
    paths:
      - data/
  only:
    - master

```