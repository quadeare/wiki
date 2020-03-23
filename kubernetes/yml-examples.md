---
title: K8s Yml file examples
description: 
published: true
date: 2020-03-23T13:18:41.744Z
tags: 
---

# Kubernetes Yml example

## Deployment

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
  labels:
    app: myapp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: myapp:1.7.9
        ports:
        - containerPort: 80
```

## Service

```yml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: myapp
  name: myapp
spec:
  type: NodePort
  ports:
  - name: tcp
    port: 80
    nodePort: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: myapp
```

## Ingress

```yml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: myapp-ingress
  annotations:
    cert-manager.io/cluster-issuer: letsencrypt-prod
    kubernetes.io/tls-acme: "true"
    myapp.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: example.domaine.tld
    http:
      paths:
      - backend:
          serviceName: myapp
          servicePort: 80
  tls:
  - hosts:
    - example.domaine.tld
    secretName: pass-cert

```