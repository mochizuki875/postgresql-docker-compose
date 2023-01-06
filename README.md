# PostgreSQL by Docker
## 概要
dockerでPostgreSQLとpgAdminを構築する。

## 環境
```
docker compose version
Docker Compose version v2.2.1
```

## 構築
```
❯❯❯ docker compose up -d
・・・
❯❯❯ docker compose ps
NAME                    COMMAND                  SERVICE             STATUS              PORTS
1440ca7f2bec   dpage/pgadmin4         "/entrypoint.sh"         51 minutes ago   Up 51 minutes   443/tcp, 0.0.0.0:8880->80/tcp, :::8880->80/tcp   postgresql-docker-compose-pgadmin-1
6955f8df0ede   postgres:latest        "docker-entrypoint.s…"   51 minutes ago   Up 51 minutes   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp        postgresql-docker-compose-postgres-1
```

```
❯❯❯ docker exec -it postgresql-postgres-1 /bin/bash
root@7169b44f5321:/# psql -d postgres -U postgres
psql (14.2 (Debian 14.2-1.pgdg110+1))
Type "help" for help.

# データベース一覧を取得
postgres-# \l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
-----------+----------+----------+------------+------------+-----------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
(3 rows)

# 接続しているデータベースを取得
postgres=# SELECT current_database() AS database_name;
 database_name 
---------------
 postgres
(1 row)

# ユーザー一覧を取得
postgres=# select user from pg_user;
   user   
----------
 postgres
(1 row)
```

## 参考
docker composeを使ってPostgreSQLを構築する  
https://mebee.info/2020/12/04/post-24686/  

Docker postgres  
https://hub.docker.com/_/postgres
