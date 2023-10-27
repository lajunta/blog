---
title: "Mysql Basic"
date: 2021-04-06T14:14:52+08:00
draft: false
categories: ["mysql"]
---

# Add and Grand user


```bash

CREATE DATABASE database_name;

CREATE USER 'newuser'@'10.8.0.5' IDENTIFIED BY 'user_password';

GRANT ALL PRIVILEGES ON database_name.* TO 'database_user'@'localhost';

```

# Alter user password

```bash
alter user 'username'@'localhost' identified by 'user_password';
```

# Drop user

```bash
drop user 'user'@'localhost';
```