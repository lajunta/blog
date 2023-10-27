---
title: "Suid Sgid Sticky Bit"
date: 2021-04-17T09:31:33+08:00
draft: false
---

# Linux special directory/file permission setup

### SUID (+s | numercial code 4)

只有文件的所有者才能执行， 其它人不能执行 

```bash
chmod 4770 file
```

### SGID (+s | numercial code 2)

只有组的所有者才能执行，其它人不能执行

```bash
chmod  2770 file | directory
```

1. 如果设置在文件上,和suid一样，只有组的成员才能执行
2. 如果设置在目录上,目录内新建的文件都会继承所在目录的组权限

### Sticky bit (+t | numercial code 1)

只能加在目录上,目录内的文件,只有其所有者才能删除

```bash
  chmod 1777 file
```

```bash
[one@server test]$ ls -ld /tmp/
drwxrwxrwt. 15 root root 4096 Sep 28 19:28 /tmp/
```
