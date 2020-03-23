---
title: RBAC management snippets
description: 
published: true
date: 2020-03-23T14:40:02.330Z
tags: 
---

# RBAC management snippets

## Generate user key
```bash
openssl genrsa -out <user>.key 2048
```

## Generate <user>.csr from previous key

```bash
openssl req -new \
    -key <user>.key \
    -out <user>.csr \
    -subj "/CN=<user>/O=<group>"
```

## Go to certificates path

## Generate certificate from csr file

```bash
openssl x509 -req \
    -in <user>.csr \
    -CA ca.crt \
    -CAkey ca.key \
    -CAcreateserial \
    -out <user>.crt \
    -days 360
```

```bash
kubectl config set-credentials <user> \
    --client-certificate=<user>.crt \
    --client-key=<user>.key
```

```bash
kubectl config set-context <user>-context \
    --cluster=kind-kind \
    --namespace=default \
    --user=<user>
```

## Go to <user>-context (All will be forbiden)

```bash
kubectl get pods 
kubectl create namespace another-namespace 
```

## Now create a Role

```yml
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  namespace: default
  name: get-pods
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```

## And RoleBinding

```yml
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: get-pods
  namespace: default
subjects:
- kind: User
  name: <user>
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: get-pods
  apiGroup: rbac.authorization.k8s.io
```
  
# Another main menu
  
## Another sub menu