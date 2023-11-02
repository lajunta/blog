---
title: "Using Age Crypt|Decrypt"
date: 2023-11-02T18:37:41+08:00
draft: false
---

Using Age to Crypt|Decrypt 
===

age 是使用go语言开发的一个文件加密软件，按官方说法：

> 一种简单、现代和安全的加密工具，具有无配置选项，可使用公钥来明确指定接收人, 兼容UNIX风格的特性
官方地址：https://github.com/FiloSottile/age

## 使用短语加密解密文件

```bash
age -e -p -o hello.age hello.tar.xz
输入密码后会对文件 hello.tar.xz 加密，并生成 hello.age
age -d -o hello.tar.xz hello.age
解开文件并指定解开的文件名为 hello.tar.xz
```

## 使用密钥进行加密解密

1. 生成密钥对

```bash
age-keygen -o key.txt
Public key: age1d2xf7rk9yj5a7eul38kcfc7j09ykhn9hw2hzzawrjjnus7dwrf6s68pl4t
```

2.  使用上面生成的公钥进行加密

```bash
tar cvz ./data | age -r age1d2xf7rk9yj5a7eul38kcfc7j09ykhn9hw2hzzawrjjnus7dwrf6s68pl4t > data.tar.gz.age
```

3. 使用私钥进行解密

```bash
age -d -i key.txt -o data.tar.gz data.tar.gz.age
tar xf data.tar.gz
```

### age 用法

```bash
age -e -p -o 加密文件 未加密文件
age -e -r 公钥1 -r 公钥2 -o 加密文件 未加密文件
age -d [-i 私钥文件] -o 解密后文件 加密文件
```

### age 选项

```bash
-e 加密，默认不用写
-d 解密
-o 输出的文件名
-p 使用短句加密
-i 私钥文件，解密用
-r 公钥，加密用
-a 使用PEM编码格式进行加密
```

age 总的来说使用非常简单，可用二种方式加密，其中第二种密钥方式更加安全，参数也不多，是一个很好的加密工具。

