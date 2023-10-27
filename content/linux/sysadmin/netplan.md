---
title: "Linux Netplan"
date: 2021-04-06T14:17:04+08:00
draft: false
tags: ["linux","sysadmin"]
---
Netplan config
===

`/etc/netplan/01-netcfg.yaml`

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp3s0:
      dhcp4: no
      dhcp6: no
      addresses: [172.16.145.240/24]
      #gateway4: 172.16.145.254
      nameservers:
        addresses: [172.16.1.2,172.16.145.254]
      routes:
        - to: 172.16.144.248/24
          via: 172.16.144.254
        - to: 172.16.144.249/24
          via: 172.16.144.254
        - to: 0.0.0.0/0
          via: 172.16.145.254
    enp5s0:
      dhcp4: no
      dhcp6: no
      addresses:
        - 192.168.3.254/24
        - 192.168.6.254/24
```