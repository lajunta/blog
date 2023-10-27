---
title: "Wsl Install Mongodb"
date: 2023-10-27T15:20:48+08:00
draft: false
---
WSL Install Mongodb
===

1. Import Public Key
```bash
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
```

1.  Create mongodb source file
```bash
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
```

1. Reload package 
```bash
sudo apt update
```

1. Install mongodb-org
```bash
sudo apt-get install -y mongodb-org
```

1. Add the init script

```bash
curl https://raw.githubusercontent.com/mongodb/mongo/master/debian/init.d | sudo tee /etc/init.d/mongodb >/dev/null
```

1. Add permission

```bash
sudo chmod +x /etc/init.d/mongodb
```

1. Solve some dbpath and permission issues;

1. Start the mongodb 

```bash
sudo service mongodb start
```