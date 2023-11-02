---
title: "Transfer Fping SX"
date: 2023-11-02T18:41:23+08:00
draft: false
---

Transfer Fping And SX
===

## transfer.sh

```shell
curl --upload-file fping.zip https://transfer.sh/fping.zip

curl --upload-file sx https://transfer.sh/sx
```

## fping

```shell
fping -a -g 192.168.1.0/24 2>/dev/null
```

## sx

```shell
sx arp 192.168.1.0/24
```
