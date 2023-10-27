---
title: "生成随机数"
date: 2021-04-06T14:15:57+08:00
draft: false
tags: ["linux","commands"]
---
生成随机数
===

xxd
---

```bash
xxd -g 2 -l 64 -p /dev/random | tr -d "\n"
```

openssl
---

```bash
openssl passwd -5 -salt xyz "yourpassword" | base64
```

head
---

```bash
cat /dev/urandom | base32 | head -c 64
```