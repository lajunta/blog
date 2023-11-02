---
title: "Vbs_Bckground_Run"
date: 2023-11-02T18:53:29+08:00
draft: false
---

VBS Background Running
===

small vbs script to run a program in background

```bash
Set WshShell = CreateObject("WScript.Shell")
cmds=WshShell.RUN("remotely.exe student", 0, True)
Set WshShell = Nothing
```