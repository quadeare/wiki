---
title: Python virtualenv
description: 
published: true
date: 2020-03-23T13:00:45.936Z
tags: 
---

# Python virtualenv usefull commands

## Install 

### Debian / Ubuntu

```bash
sudo apt install python3-pip
```

```bash
pip3 install virtualenv
pip3 install virtualenvwrapper
```

### Edit .bashrc or .zshrc

```bash
#Virtualenvwrapper settings:
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_VIRTUALENV=~/.local/bin/virtualenv
source ~/.local/bin/virtualenvwrapper.sh
```

## Usefull virtualenvwrapper commands

### Create virtualenv

```bash
mkvirtualenv <env>
```

### Copy virtualenv

```bash
cpvirtualenv <source_env> <target_env>
```

### Show virtualenv

```bash
showvirtualenv <env>
```

### List virtualenv

```bash
lsvirtualenv
```

### Use virtualenv

```bash
workon <env>
```

### Quit virtualenv

```bash
desactivate
```
