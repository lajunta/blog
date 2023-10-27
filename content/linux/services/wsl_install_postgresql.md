---
title: "Wsl Install Postgresql"
date: 2023-10-27T14:59:23+08:00
draft: false
---

Install postgres in wsl
===

> ```bash
> sudo apt update
> sudo apt install postgresql postgresql-contrib
> psql --version
> ```

## Start the service
```bash
sudo service postgresql status
sudo service postgresql start
```

## Set default admin user postgres password

```bash
sudo passwd postgres
```

## Enter the admin cli
```bash
sudo -u postgres psql
```

## See what user created
```bash
psql -c "\du"
```

## Create and drop database

```bash
sudo -u postgres createdb mydb
sudo -u postgres dropdb mydb
```

## Create and drop database

```bash
sudo -u postgres createuser  someone
sudo -u postgres createuser -W someone // give a password
sudo -u postgres dropuser someone
```

## Change user password
```bash
sudo -u postgres psql 
ALTER USER user_name WITH PASSWORD 'new_password';
```

## Grant privileges to user
```bash
GRANT ALL PRIVILEGES ON DATABASE database_name TO username;
```

## Postgresql docs

https://www.postgresql.org/docs/13/tutorial-createdb.html