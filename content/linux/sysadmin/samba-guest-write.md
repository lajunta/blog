---
title: "Samba Guest Write"
date: 2021-04-10T09:26:46+08:00
draft: false
---

## Samba Server for guest user

__smb.conf__

```bash
# Global parameters
[global]
  server string = Temp Samba Server
  netbios name = R33 
  server role = standalone server
  map to guest = bad user
  guest account = zxy
  create mode = 664 
  inherit owner=yes 
  inherit permissions=yes

[文件收集]
  path = /var/collect
  read only = no
  writeable = yes 
  write list = zxy
  public = yes
  guest ok = yes
  force user = zxy
  create mask = 0644
  directory mask = 1777
```

### File System operations 

设置文件或者文件夹 不是文件夹所在组和用户


```bash
chown -R root:emptygroup * /path/to/dir/
```

设置 sticky 位为1:

```bash
chmod -R 1777 /path/to/dir/
```


```bash
inherit owner=yes
inherit permissions=yes
```
