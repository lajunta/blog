---
title: "Disable_windows10_update"
date: 2023-10-27T14:43:05+08:00
draft: false
tags: ["windows","tips"]
---

Disable Windows Update
===

##  禁止windows更新服务

在恢复选项卡中， 把第一次失败后 操作 改为 无操作 ， 应用

## 禁止计划任务

在我的电脑->管理->计划任务->Microsoft->Windows下把计划任务改为禁止

## 通过组策略禁止

运行 `gpedit.msc`

- 计算机配置 - 管理模板 - Windows 组件 - Windows 更新 - 配置自动更新  更改为已禁用

 - 通知下载并通知安装 或者 你也可以直接调整为：已禁用

- 计算机配置 - 管理模板 - Windows 组件 - Windows 更新 - 指定 Intranet Microsoft更新服务位置，改为已启用

- 选项都为 http://127.0.0.1

## 使用注册表

- 运行 regedit

- HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU

- 如果没有 `AU` 就新建项

在 AU 下新建 DWORD 32位 `NoAutoUpdate`  值 为 1

