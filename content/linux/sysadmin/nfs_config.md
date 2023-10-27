---
title: "Nfs_config"
date: 2023-10-27T14:30:42+08:00
draft: false
---
NFS Confiｇ
===

# 修改  `/etc/exports` 文件

```bash
/mnt1  192.168.1.1(rw,fsid=0,no_subtree_check)
/mnt2  192.168.1.2(rw,fsid=0,no_subtree_check)
```

# 修改 `/etc/nfs.conf` 

```bash
[exports]
rootdir=/srv/nfs
```

# 修改 `/srv/nfs` 文件权限(需和客户端用户一样)
```bash
chown nobody:nobody /srv/nfs
```

# 防火墙添加 111  2049  20048 端口
```bash
iptables -A INPUT -p tcp -m tcp --dport 111 -j ACCEPT
iptables -A INPUT -p tcp -m tcp --dport 2049 -j ACCEPT
iptables -A INPUT -p tcp -m tcp --dport 20048 -j ACCEPT
iptables -A INPUT -p udp -m udp --dport 111 -j ACCEPT
iptables -A INPUT -p udp -m udp --dport 2049 -j ACCEPT
iptables -A INPUT -p udp -m udp --dport 20048 -j ACCEPT
```

# Archlinux 连接
```bash
https://wiki.archlinux.org/title/NFS
```