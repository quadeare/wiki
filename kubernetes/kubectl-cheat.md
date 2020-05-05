---
title: Kubectl cheat
description: 
published: true
date: 2020-05-05T07:31:55.453Z
tags: 
---

# Kubectl cheat commands

Sources : Get from https://linuxacademy.com/blog/containers/kubernetes-cheat-sheet/

## Get ressources informations

### Nodes

```bash
kubectl get no
kubectl get no - o wi de
kubectl descr i be no
kubectl get no - o yaml
kubectl get node --selector=[label_name]
kubectl get nodes -o jsonpath=' { .items[*].status. addresses[?(@.type=="ExternalIP")].address}'
kubectl top node [ node_name]
```