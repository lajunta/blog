---
title: "Sync_and_restore"
date: 2023-11-02T18:50:43+08:00
draft: false
---

Sync And Restore file
===

```bash
#!/bin/bash

lwqzxfile="/data/lwqzxfile"
lwqzxdb="/data/lwqzxdb"
db="lwqzx"

if [ $1 = "file" ]; then
  echo "Start backup lwqzx file data....."
  rsync -e 'ssh -p 22' -avz ecole:/home/zxy/apps/lwqzx/ $lwqzxfile
  sleep 1
  echo "$(date +'%Y:%m:%d %H:%M') - Lwqzx file data is synced!"
fi

if [ $1 = "db" ];then
  echo "----------------------------------"
  echo "Start backup lwqzx database ...."
  rsync -e 'ssh -p 22' -avz ecole:/data/mariadbak/ $lwqzxdb
  echo "$(date +'%Y:%m:%d %H:%M') - Ecole mariadb synced!"
fi

if [ $1 = "restore" ];then
  echo "Restore today($(date +%u)) data"
  gzfile=$lwqzxdb/DAILY/$(date +%u)_lwqzx.gz
  dumpfile=/tmp/$(date +%u)_lwqzx_dump
  gzip -c -k -d $gzfile | mysql -u lwqzx -D lwqzx -p  
  #mysql -u lwqzx -p < dumpfile
  echo "$(date +'%Y:%m:%d %H:%M') - Data restored!"
fi
```

