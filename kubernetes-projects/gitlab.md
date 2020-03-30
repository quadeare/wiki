---
title: Giltab K8S deployment
description: 
published: true
date: 2020-03-30T13:15:23.100Z
tags: 
---

# Gitlab K8S deployment notes

## Somes links

Gitlab architecture and components list : https://docs.gitlab.com/ce/development/architecture.html#component-list

Gitlab chart documentation : https://docs.gitlab.com/charts/

## Gitlab hem chart dependencies

Postgres : https://github.com/bitnami/charts/tree/master/bitnami/postgresql
Redis : https://github.com/bitnami/charts/tree/master/bitnami/redis


## Storage types

URL : https://docs.gitlab.com/ee/administration/repository_storage_types.html


## Helm task - Use legacy storage

### Switch storage to legacy mode

![selection_028.png](/kubernetes-projects/gitlab/selection_028.png)

### Customize volume claim

URL : https://gitlab.com/gitlab-org/charts/gitlab/-/blob/v3.2.1/charts/gitlab/charts/gitaly/templates/statefulset.yml#L186