---
title: "Project_venv_setup"
date: 2023-11-02T11:21:27+08:00
draft: false
---

python Venv Setup
===

### Install python3-venv

```bash
sudo apt-get install python3-venv
```bash

### Create a project folder and a venv folder within

```bash
$ mkdir myproject
$ cd myproject
$ python3 -m venv venv
```

### Activate the environment

```bash
$ . venv/bin/activate
```

### Install Flask

```bash
$ pip install Flask
```