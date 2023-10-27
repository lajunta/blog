---
title: "Win11 Visit Shared Printer"
date: 2023-10-27T14:45:40+08:00
draft: false
---

Win11 Visit Shared Printer
===

# Make gpedit.msc work

```bash
winver

sfc /scannow

# repair windows image

Dism /Online /Cleanup-Image /RestoreHealth
```

# How to Enable group policy editor in windows 11 home

```bash
@echo off 
pushd "%~dp0"
dir /b %SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientExtensions-Package~3*.mum >List.txt 
dir /b %SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientTools-Package~3*.mum >>List.txt 
for /f %%i in ('findstr /i . List.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"
pause
```
# Modify registry for win11 enable install shared printer

How To Solved operation could not be completed error 0x709 Fix windows 11 & 10

## 打开 windows 特性 

- LPD Printer Service
- LPR Port Monitor

## 配置本地组策略

Local Group Policy Editor
本地计算机策略 计算机配置 管理模板 打印机 
Administrative Templetes  Printer

- Configure RPC Connection - Enabled- RPC over named pipes
- Configure RPC Listener - Enabled- RPC over named pipes and TCP
- Configure RPC over TCP - Enabled

## 使用注册表
[HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows NT\Printers\RPC]
create if not existed

DWORD (32 bit) Value
- ForceKerberosForRpc 0
- RpcAuthentication 0
- RpcProtocols  7
- RpcTcpPort 0
- RpcOverTcp 0
- RpcOverNamedPipes 1
- RpcUseNamedPipeProtocol 1

## 授权

HKEY_CURRENT_USER\Software\Microsoft\WindowsNT\CurrentVersion\Windows
Then Right-click on Windows key and select Permissions.

give all application pacages  Full Control and Read

## RpcAuthnLevelPrivacyEnabled 新增为 0
DWORD (32 bit) Value
 [HKEY_LOCAL_MACHINE\SYSTEM|CurrentControlSet\Control\Print

## 启动服务

- Print Spooler

