---
title: "Wsl Install Mariadb"
date: 2023-10-27T14:57:53+08:00
draft: true
---

WSL Install Mariadb
==

```bash
sudo rm /var/lib/mysql/* -rf
sudo apt install mariadb-server
sudo -u mysql mysql_install_db
```

## Start mariadb

```bash
sudo service mariadb start
```