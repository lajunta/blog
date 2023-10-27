---
title: "Printer Share Using Samba On Ubuntu"
date: 2021-06-29T16:40:14+08:00
draft: false
---

## Printer Share On Ubuntu

### Edit smb.conf

```bash
[printers]
   comment = All Printers
   browseable = no
   path = /var/spool/samba
   printable = yes 
   guest ok = no
   read only = yes 
   create mask = 0700
   valid users = dayin

[print$]
   comment = Printer Drivers
   path = /var/lib/samba/printers
   browseable = yes 
   read only = yes 
   guest ok = no
   valid users = dayin
```

### Add user dayin

```bash
sudo useradd -M -N -s /bin/false -d /nonexsistent dayin 
sudo smbpasswd -a dayin
```

### Add creditial on windows

```bash
ip: server ip
user: dayin
psd: smbpasswd for dayin
```