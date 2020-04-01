---
title: Helm
description: 
published: true
date: 2020-04-01T08:14:01.051Z
tags: 
---

# Helm

## Basic commands

### List Helm deployments

```bash
helm list
```

#### With all namespaces

```bash
helm list --all-namespaces
```

### List repo

```bash
helm repo list
```

### Update repo

```bash
helm repo update
```

### Fetch latest revision for specific chart

```bash
helm fetch <repo_name>/<chart>
```

Example with Rancher :

```bash
helm fetch rancher-stable/rancher
```

### Get values for helm deployment

```bash
helm get values <helm_deployment>
```

### Helm upgrade deployment

```bash
helm upgrade <deployment_name> <repo_name>/<chart> --set <key>=<value> -n <namespace>
```

#### Example with Rancher

```bash
helm upgrade rancher rancher-stable/rancher \
--set hostname=rancher.cheezecake.ovh -n cattle-system
```

#### Example with cert-manager

```bash
helm upgrade cert-manager jetstack/cert-manager -n cert-manager
```