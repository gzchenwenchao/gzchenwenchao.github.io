---
layout: post
title:  "PostpreSQL 安装&基本使用"
date:   2017-10-21 17:45:00 +0800
categories: code
---

postgresql 安装（安装部分基本转载自：http://dhq.me/mac-postgresql-install-usage）

1. 安装：brew install postgresql
2. 初始化：initdb /usr/local/var/postgres -E utf8
3. 启动：pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log start
4. 关闭：pg_ctl -D /usr/local/var/postgres stop
5. 创建用户：createuser ${username} -P
6. 创建数据库：createdb ${databasename} -O ${ownername} -E UTF8 -e
7. 连接数据库：psql -U ${username} -d ${databasename} 127.0.0.1
8. psql命令：

```
显示已创建的数据库：\l
连接数据库：\c dbname
显示数据库表：\d
创建一个名为test的表：CREATE TABLE test (id int, text VARCHAR(50));
插入一条记录：INSERT INTO test(id, text) VALUES(1, 'test');
查询记录：SELECT * FROM test WHERE id = 1;
更新记录：UPDATE test SET text = 'aaaaaaaaaaaaa' WHERE id = 1;
删除指定的记录：DELETE FROM test WHERE id = 1;
删除表：DROP TABLE test;
删除数据库：DROP DATABASE dbname;
备份：pg_dump dbname > /usr/local/psql/backup/pg.sql
恢复：psql newdb < /usr/local/psql/backup/pg.sql
```

建表demo

```sql
CREATE TABLE user0(
    id SERIAL,--自增长
    username varchar(64) UNIQUE,
    update_time timestamp
);
```

insert demo

```sql
insert into user0(username, update_time) values('test', now());
```

node 安装 postgresql module（参考http://expressjs.com/en/guide/database-integration.html#postgresql）

$ npm install pg-promise

node 操作 postgresql 参考材料：https://www.npmjs.com/package/pg-promise#query-formatting