---
title: "Hide App From Installed Applications"
date: 2023-10-27T14:33:22+08:00
draft: false
tags: ["tips","windows"]
---
Hide App From Installed Applications
===

## Understanding entries
You can hide the entry about the installed application through the Windows registry. But first of all, you need to understand how Windows builds the list of installed programs that you see in the Control Panel. You can find information about the installed application in one of three registry keys:

A general list of programs for all users of a device;

> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall 

Following registry key contains entries about x86 apps installed on x64 Windows builds;

> HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall 

This next registry contains apps installed for the current user only.

> HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Uninstall 


Windows generates the list of installed programs that you see in the Settings or Control Panel based on the entries in these registry keys.

In this case, the GIMP is installed via the Winget package manager only to my user profile, so its entry is inside the user registry hive 

> HKCU\Software\Microsoft\Windows\CurrentVersion\Uninstall.

Find the application reg key (in my example it is GIMP-2_is1) and create a new 32-bit DWORD registry parameter with the name SystemComponent and 

> value 1: SystemComponent = dword: 00000001