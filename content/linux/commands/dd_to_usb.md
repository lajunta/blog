---
title: "Dd_to_usb"
date: 2023-11-02T18:42:57+08:00
draft: false
---

用DD写入ISO到USB
===


```bash
sudo dd bs=4M if=Downloads/ubuntu-19.04-desktop-amd64.iso of=/dev/sdb conv=fdatasync status=progress
```

### 说明

> **dd**:  The name of the command we’re using.
>
> **bs=4M**:  The -bs (blocksize) option defines the size of each chunk that is read from the input file and wrote to the output device. 4 MB is a good choice because it gives decent throughput and it is an exact multiple of 4 KB, which is the blocksize of the ext4 filesystem. This gives an efficient read and write rate.
> 
> **if** =Downloads/ubuntu-19.04-desktop-amd64.iso: The -if (input file) option requires the path and name of the Linux ISO image you are using as the input file.
>
> **of=/dev/sdb** : The -of (output file) is the critical parameter. This must be provided with the device that represents your USB drive. This is the value we identified by using the lsblk command previously. in our example it is sdb, so we are using /dev/sdb. Your USB drive might have a different identifier. Make sure you provide the correct identifier.
>
> **conv=fdatasync** : The conv parameter dictates how dd converts the input file as it is written to the output device. dd uses kernel disk caching when it writes to the USB drive. The fdatasync modifier ensure the write buffers are flushed correctly and completely before the creation process is flagged as having finished.