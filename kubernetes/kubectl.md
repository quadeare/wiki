---
title: Kubectl tricks
description: 
published: true
date: 2020-03-24T10:24:11.288Z
tags: 
---

# Kubectl tricks

## Common

### Multiple contexts example

```bash
export KUBECONFIG=$HOME/.kube/config:$HOME/.kube/config2:$HOME/.kube/config3
```

### Get server and client verion

```bash
kubectl version
```

## Manifests

## Apply manifest

```bash
kubectl apply -f <manifest>.yml
```

### Generic command :

```bash
kubectl create $(OBJECT_TYPE) $(OBJECT_TYPE_OPTIONS) $(RESOURCE_NAME) --dry-run -o yaml > manifest.yaml
```

### Deployment example :

```bash
kubectl create deployment busybox-test --image=busybox --dry-run -o yaml > deployment.yaml
```

### Configmap example :

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

### Taints

#### Taint a node

```bash
kubectl taint nodes <NODE> key=<VALUE>:<TAINT_EFFECT>
```

* **NoSchedule** : Pods that do not tolerate this taint are not scheduled on the node.
* **PreferNoSchedule** : Kubernetes avoids scheduling Pods that do not tolerate this taint onto the node.
* **NoExecute** : Pod is evicted from the node if it is already running on the node, and is not scheduled onto the node if it is not yet running on the node.


## Contexts

### Get current context

```bash
kubectl config current-context
```

### Get all contexts

```bash
kubectl config get-contexts
```