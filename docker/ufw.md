---
title: UFW Docker
description: 
published: true
date: 2020-03-23T15:38:36.886Z
tags: 
---

# UFW with Docker

## Introduction

> The default firewall configuration tool for Ubuntu is ufw. Developed to ease iptables firewall configuration, ufw provides a user friendly way to create an IPv4 or IPv6 host-based firewall.
{.is-info}

## Use UFW with Docker

### Disable Docker iptables

Create or edit `/etc/docker/daemon.json` :

```json
{
        "iptables": false,
        "dns": ["213.186.33.99"]
}
```

Restart Docker engine :

```bash
sudo systemctl restart docker
```

### UFW configuration

1. Edit `/etc/default/ufw` :

* Change `DEFAULT_FORWARD_POLICY` value to `ACCEPT`

2. Edit `/etc/ufw/before.rules` :

Add the following content **BEFORE** `*filter` :

```bash
*nat
:POSTROUTING ACCEPT [0:0]
-A POSTROUTING ! -o docker0 -j MASQUERADE
COMMIT
```

3. Allow communication between containers

```bash
ufw allow from 172.17.0.0/16
```

4. Add all your rules before ufw apply

SSH example :

```bash
sudo ufw allow ssh
```

5. Reload UFW service

```bash
sudo ufw reload
```

> Warning : Check UFW rules before apply. You can lost connection on critical services (SSH, Web etc...)
{.is-warning}


