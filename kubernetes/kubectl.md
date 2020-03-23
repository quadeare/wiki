---
title: Kubectl tricks
description: 
published: true
date: 2020-03-23T15:20:13.104Z
tags: 
---

# Kubectl tricks

## Common

### Multiple contexts example

```bash
export KUBECONFIG=$HOME/.kube/config:$HOME/.kube/config2:$HOME/.kube/config3
```

### Generate manifest template

#### Generic command :

```bash
kubectl create $(OBJECT_TYPE) $(OBJECT_TYPE_OPTIONS) $(RESOURCE_NAME) --dry-run -o yaml > manifest.yaml
```

#### Deployment example :

```bash
kubectl create deployment busybox-test --image=busybox --dry-run -o yaml > deployment.yaml
```

#### Configmap example :

```bash
kubectl create configmap configmap-test --dry-run -o yaml > config-map.yaml
```

## Cluster

### Get cluster status

```bash
kubectl get componentstatus
```

### Get node list

```bash
kubectl get nodes
```

## Contexts

### Get current context

```bash
kubectl config current-context
```

### Get all contexts

```bash
kubectl config get-contexts
```