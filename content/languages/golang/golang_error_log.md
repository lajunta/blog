---
title: "Golang Custoum Error Log"
date: 2023-11-02T18:39:46+08:00
draft: false
---

Golang Create Error Log File
===

创建文件 
```bash
ErrLogFile, _ = os.OpenFile("errors.log", os.O_APPEND|os.O_CREATE|os.O_RDWR, 0755)
```

指定日志输出到文件

```bash
ErrLOG = log.New(ErrLogFile, "Error:", log.Ldate|log.Ltime|log.Lshortfile)
```

把日志输出到文件
```bash
ErrLOG.Println(something error)
```
