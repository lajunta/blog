---
title: "Samba Ports Firewall"
date: 2023-11-02T18:52:07+08:00
draft: false
---

Samba ports for firewall
===


The CIFS server ports that have to be network enabled to accept traffic from the client are:

1. Browsing datagram responses of NetBIOS over TCP/IP: 138/UDP
1. Browsing requests of NetBIOS over TCP/IP: 137/UDP
1.  Client/Server Communication: 135/TCP
1. Common Internet File System (CIFS): 445/UDP and 139,44/TCP