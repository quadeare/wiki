---
title: Public folder Linux
description: 
published: true
date: 2020-03-23T11:22:51.032Z
tags: 
---

# Public folder Linux

Very simple snippet to create a public folder on Linux :

```bash
sudo mkdir /home/public
sudo groupadd share
sudo chown -R root:share /home/public
sudo chmod ug+rwx -R /home/public
sudo chmod g+s /home/public
```

Link from github : https://gist.github.com/quadeare/8f93d72a97b079b38f34bd0f0297d72c


Use it with curl or wget :

```bash
curl -fsSL https://bit.ly/3dlscZ3 | sh
```

