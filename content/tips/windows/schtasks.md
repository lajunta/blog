---
title: "Schtasks"
date: 2023-11-02T18:47:44+08:00
draft: false
---

Using Schtasks 
===

## Create task from xml
```bash
schtasks /Create [/S <system> [/U <username> [/P [<password>]]]] /XML <xmlfile> /TN <taskname>
```

## Disable enable a task

```bash
schtasks /Change /TN "KMS10" /Disable
```

## Delete a task
```bash
schtasks /Delete /TN "KMS10" /F
```

## End a task
```bash
schtasks /END /TN "KMS10"
```