---
title: "Iperf3 Lan Speed Test"
date: 2023-11-02T18:49:02+08:00
draft: false
---

Using Iperf3
===

### start the server on port 5001

```bash
iPerf3 -s
```

### start the server on another port
```bash
iPerf3 -s -p 7575
```

### start the client on port 7575

```bash
iPerf3 -c 10.10.10.1 -p 7575
```

### start upload and download test 
```bash
iPerf3 -c 10.10.10.1 -p 7575 -bidir
```

### logfile
```
iPerf3 -c 10.10.10.1 -p 7575 -bidir --logfile c:\users\administrator\desktop\speedtest.txt
```