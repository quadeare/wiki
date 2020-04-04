---
title: Rclone
description: 
published: true
date: 2020-04-04T21:08:59.714Z
tags: 
---

# Rclone

## Google Drive

```bash
[Unit]
Description=Rclone Mount Gsuite
After=network-online.target
Wants=network-online.target
 
[Service]
Type=notify
ExecStart=/usr/bin/rclone mount gcrypt: /mnt/storage \
   --allow-other \
   --buffer-size 32M \
   --dir-cache-time 128h \
   --drive-chunk-size 32M \
   --log-file /var/log/rclone-gdrive-encrypt.log \
   --vfs-read-chunk-size 64M \
   --vfs-read-chunk-size-limit off \
   --rc 
ExecStop=/bin/fusermount -uz /mnt/storage
Restart=on-abort
User=<user>
Group=<group>

[Install]
WantedBy=gmedia.service
```


Use personal API key : https://rclone.org/drive/#making-your-own-client-id

Use cache feature : https://rclone.org/cache/