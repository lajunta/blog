---
title: "Cloudflared Tunnel"
date: 2023-10-27T15:17:22+08:00
draft: false
---

Cloudflare tunnel mini tutorial
===
# cloudflare tunnel mini tutorial


## Login 

```bash
cloudflared tunnel login
```
## Create tunnel

```bash
cloudflared tunnel create <tunnel name>
```

## Setup configuration yaml

under $HOME/.cloudflared/

make a yaml file like hello.yml

contents like this:

```yml
tunnel: <tunnel uuid>                                          
credentials-file: /home/zxy/.cloudflared/<tunnel uuid>.json    
                       
ingress:                                                                              
  - hostname: app1.domain.com                                                          
    service: ssh://localhost:22                                                  
  - hostname: app2.domain.com                                                          
    service: http://localhost:9001                                                    
  - hostname: app3.domain.com                                                   
    service: http://localhost:12345                                                   
  - service: http_status:404
```

## Publish Service

```bash
cloudflared tunnel route dns <tunnel uuid> app1.domain.com
```

## Run The tunnel

last hello is the tunnel name

```bash
cloudflared tunnel --no-autoupdate --config /home/one/.cloudflared/hello.yml run hello 
```

## Add application 

this step make some visit methods to your  app

## A Service file

```text
[Unit]
Description=Tunnel Service
After=network.target

[Service]
Type=simple
User=one
WorkingDirectory=/home/one/tmp
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/cloudflared tunnel --no-autoupdate --config /home/one/.cloudflared/hello.yml run hello

[Install]
WantedBy=multi-user.target
```

## How to visit a ssh host

add following to .ssh/config

```bash
Host your.domain.com
ProxyCommand cloudflared access ssh  --hostname your.domain.com
User one
```