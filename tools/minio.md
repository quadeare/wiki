---
title: Minio : Some usefull commands...
description: 
published: true
date: 2020-03-23T11:03:19.061Z
tags: 
---

# Introduction

Minio is a cloud native open-source object storage solution (S3 compatible). Here, you can found some usefull commands to administrate your Minio instance.

## Start ‘mc’ command by using Docker command

```bash
docker run -it --rm -entrypoint=/bin/sh minio/mc:<TAG>
```

```bash
docker run -it --rm -entrypoint=/bin/sh minio/mc:RELEASE.2019-09-11T19-53-16Z
```

Warning Be careful when you choose minio/mc tag. Please, choose tag timestamp equal to the minio server.

## Login to minio instance

```bash
mc config host add <ALIAS> <YOUR-S3-ENDPOINT> <YOUR-ACCESS-KEY> <YOUR-SECRET-KEY> <API-SIGNATURE>
```

```bash
mc config host add minio https://minio.myhostingservice.com/ admin <YOUR-SECRET-KEY>
```

## List all Minio buckets

```bash
mc ls <minio_alias>
```

```bash
mc ls minio
```

## List Minio users

```bash
mc admin user list <minio_alias>
```

```bash
mc admin user list minio
```

## List Minio policy

```bash
mc admin policy list <minio_alias>
```
```bash
mc admin policy list minio
```

## Create Minio policy

Create <your-policy>.json file (this is an example)

```json
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Sid":"yourapp",
         "Effect":"Allow",
         "Action":[
            "s3:*"
         ],
         "Resource":[
            "arn:aws:s3:::yourapp/*"
         ]
      }
   ]
}
```
  
## Apply your policy on minio instance
  
```bash
mc admin policy add <alias_minio> <policy> <policy>.json
```
```bash
mc admin policy add minio mysuperproject mysuperproject.json
```

## Add Minio user

```bash
mc admin user add myminio <user> <password>
```
```bash
mc admin user add myminio newuser newuser123
```
  
## Apply Minio policy on user

```bash
mc admin policy set <minio_alias> <policy> user=<user>
```

```bash
mc admin policy set minio mysuperproject user=newuser
```