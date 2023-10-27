---
title: "Wireguard"
date: 2021-06-07T08:34:10+08:00
draft: false
---

# wireguard

### Links

1. [Archlinux Wireguard Tutorial](https://wiki.archlinux.org/title/WireGuard) 

2. [VPN Server](https://wiki.archlinux.org/title/WireGuard#Specific_use-case:_VPN_server)

### 配置网络界面

```bash
ip link add dev wg0 type wireguard
```

1. 增加IP地址

```bash
ip address add dev wg0 192.168.88.1/24

# 如果只是二个电脑相联
ip address add dev wg0 192.168.88.1 peer 192.168.88.2
```

2. 通过配置文件进行配置

```bash
  wg setconf wg0 myconfig.conf
```

3. 激活界面

```bash
ip link set up dev wg0
```

### 查看显示界面

```bash
  wg
  wg show
  wg showconf
```

### 生成钥匙

生成私钥

```bash
  umask 077
  wg genkey > privatekey
```

生成公钥

```bash
  wg pubkey < privatekey > publickey
  or
  wg genkey | tee privatekey | wg pubkey > publickey
```

### VPN Server


server config /etc/wireguard/wg0.conf

```bash
[Interface]
Address = 10.200.200.1/24
ListenPort = 51820
PrivateKey = SERVER_PRIVATE_KEY

# substitute eth0 in the following lines to match the Internet-facing interface
# if the server is behind a router and receives traffic via NAT, these iptables rules are not needed
PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -A FORWARD -o %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -D FORWARD -o %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

[Peer]
# peer foo
PublicKey = PEER_FOO_PUBLIC_KEY
PresharedKey = PRE-SHARED_KEY
AllowedIPs = 10.200.200.2/32

[Peer]
# peer bar
PublicKey = PEER_BAR_PUBLIC_KEY
PresharedKey = PRE-SHARED_KEY
AllowedIPs = 10.200.200.3/32
```

__启动\停止server__

```
wg-quick up wg0
wg-quick down wg0
```

### VPN Client

foo client

```bash
[Interface]
Address = 10.200.200.2/32
MTU = 1420
PrivateKey = PEER_FOO_PRIVATE_KEY
DNS = 10.200.200.1

[Peer]
PublicKey = SERVER_PUBLICKEY
PresharedKey = PRE-SHARED_KEY
Endpoint = my.ddns.example.com:51820
AllowedIPs = 0.0.0.0/0, ::/0
```

bar client

```

[Interface]
Address = 10.200.200.3/32
MTU = 1420
PrivateKey = PEER_BAR_PRIVATE_KEY
DNS = 10.200.200.1

[Peer]
PublicKey = SERVER_PUBLICKEY
PresharedKey = PRE-SHARED KEY
Endpoint = my.ddns.example.com:51820
AllowedIPs = 0.0.0.0/0, ::/0
```

使用 AllowedIPs = 0.0.0.0,::/0, 在VPN上转发所有ipv4 ipv6流量