---
title: K8s Yml file examples
description: 
published: true
date: 2020-03-23T15:47:27.173Z
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

## Config map

```yml
kind: ConfigMap 
apiVersion: v1 
metadata:
  name: example-configmap 
data:
  config.yml: |-
    administration:
      authentication:
        enabled: false
```

## Secret

### Base64 encoding

```bash
echo -n 'admin' | base64
YWRtaW4=
echo -n '1f2d1e2e67df' | base64
MWYyZDFlMmU2N2Rm
```

### Secret yml example

```bash
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque
data:
  username: YWRtaW4=
  password: MWYyZDFlMmU2N2Rm
```