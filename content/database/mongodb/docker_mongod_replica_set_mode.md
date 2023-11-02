---
title: "Docker_mongod_replica_set_mode"
date: 2023-11-02T11:27:13+08:00
draft: false
---


Docker Mongod Replica Set Mode
===

```bash

[Unit]
Description=Docker Mongodb Replca
Requires=network.target
After=network.target

[Service]
User=ubuntu
Group=ubuntu
ExecStart=/usr/bin/docker run --rm --entrypoint "/usr/bin/mongod" \
            --name mongo -p 27017:27017 -v /home/ubuntu/mongodb_ecole:/data/db \
            --hostname dc.ecole \
            --add-host dc.ecole:172.16.144.248 \
            --add-host r41.ecole:172.16.143.240 \
            --add-host r33.ecole:172.16.144.240 \
            --add-host main.ecole:172.16.144.249 \
            mongo:4.4.1 --bind_ip 0.0.0.0 --replSet ecole

Type=simple
KillMode=process
Restart=on-failure
RestartSec=20s

[Install]
WantedBy=multi-user.target
```
