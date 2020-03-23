---
title: Docker-compose
description: 
published: true
date: 2020-03-23T13:24:37.985Z
tags: 
---

# Docker-compose

## Docker-compose yml example

```yml
version: "3"
services:

  app:
    image: myapp/app:v2
    depends_on:
      - db
    labels:
      traefik.enable: true
      traefik.http.routers.app.rule: Host(`app.domain.tld`)
      traefik.http.routers.app.entrypoints: web
      traefik.http.routers.app.middlewares: https_redirect

      traefik.http.routers.appsecure.rule: Host(`app.domain.tld`)
      traefik.http.routers.appsecure.entrypoints: websecure
      traefik.http.routers.appsecure.tls: true
      traefik.http.routers.appsecure.tls.certresolver: mytlschallenge

      traefik.http.middlewares.https_redirect.redirectscheme.scheme: https
      traefik.http.middlewares.https_redirect.redirectscheme.permanent: true
 
    environment:
      ENV_1: db
      ENV_2: password
    restart: unless-stopped
    networks:
      default:
      traefik:
    ports:
      - "80:3000"
      - "8080:4000"
    
  db:
    image: postgres:11-alpine
    environment:
      ENV_1: db
      ENV_2: password
    logging:
      driver: "none"
    restart: unless-stopped
    volumes:
      - data:/data
      - ./localfolder:/local
    networks:
      default:

volumes:
  data:

networks:
    default:
    traefik:
      external: true
```