---
title: K8s Yml file examples
description: 
published: true
date: 2020-03-24T19:50:31.965Z
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

## Pod

### Simple Pod

```yml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: busybox
    command: ['sh', '-c', 'echo Hello Kubernetes! && sleep 3600']
    env:
      - name: ENV_VARIABLE
        value: "Hello Kubernetes!"
```

### Pod with fieldRef

```yml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: busybox
    command: ['sh', '-c', '$MESSAGE && sleep 3600']
  env:
    - name: MESSAGE
      valueFrom:
        fieldRef:
          fieldPath: "status.hostIP"
```

> **fieldRef possible values :**
> 
> * metadata.name - the pod’s name
> * metadata.namespace - the pod’s namespace
> * metadata.uid - the pod’s UID, available since v1.8.0-alpha.2
> * metadata.labels - all of the pod’s labels, formatted as label-key="escaped-label-value" with one label per line
> * metadata.annotations - all of the pod’s annotations, formatted as annotation-key="escaped-annotation-value" with one annotation per line
> * status.podIP - the pod’s IP address
> * spec.serviceAccountName - the pod’s service account name, available since v1.4.0-alpha.3
> * spec.nodeName - the node’s name, available since v1.4.0-alpha.3
> * status.hostIP - the node’s IP, available since v1.7.0-alpha.1
{.is-success}


### Pod with resourceFieldRef
  
```yml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: busybox
    command: ['sh', '-c', '$MESSAGE && sleep 3600']
  env:
    - name: MESSAGE
      valueFrom:
        resourceFieldRef:
          resource:: "requests.cpu"
```

> **resourceFieldRef support :**
> 
> * limits.cpu
> * limits.memory
> * limits.ephemeral-storage
> * requests.cpu
> * requests.memory
> * requests.ephemeral-storage

{.is-success}

### Pod with toleration

K8s doc : https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/

```yml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: busybox
    command: ['sh', '-c', 'echo Hello Kubernetes! && sleep 3600']
  tolerations:
  - key: "mykey"
    operator: "Exists"
    effect: "NoSchedule"
```

> An **empty key** with operator **Exists** matches all keys, values and effects which means **this will tolerate everything**.
> 
> ```yml
> tolerations:
> - operator: "Exists"
> ```
> 
> An **empty effect** matches all effects with **key key**.
> 
> ```yml
> tolerations:
> - key: "key"
>   operator: "Exists"
> ```
{.is-info}


### Pod with registry secret

```yml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: myreg:5000/busybox
    command: ['sh', '-c', 'echo Hello Kubernetes! && sleep 3600']
  imagePullSecrets:
  - name: "myreg-secret"
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