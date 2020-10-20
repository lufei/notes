# PostgreSQL

PostgreSQL 是一个免费的对象-关系数据库服务器(ORDBMS)，在灵活的BSD许可证下发行。

## 安装

```bash
brew install postgresql
```

## 启动

```bash
brew services start postgresql
```

## 初始化

```bash
initdb /usr/local/var/postgres
```
然后来创建数据库和账户，Mac 安装 PostgreSQL 后不会创建用户名数据库，执行命令：

```bash
createdb
```

然后登录 PostgreSQL 控制台：

```bash
psql
```
psql 连接数据库默认选用的是当前的系统用户

## 其他操作

### 创建 postgres 用户

```bash
CREATE USER postgres WITH PASSWORD '密码';
```

### 删除默认生成的 postgres 数据库

```bash
DROP DATABASE postgres;
```

### 创建属于 postgres 用户的 postgres 数据库

```bash
CREATE DATABASE postgres OWNER postgres;
```

### 将数据库所有权限赋予 postgres 用户

```bash
GRANT ALL PRIVILEGES ON DATABASE postgres to postgres;
```

### 给 postgres 用户添加创建数据库的属性

```bash
ALTER ROLE postgres CREATEDB;
```

这样就可以使用 postgres 作为数据库的登录用户了，并可以使用该用户管理数据库了

## 登陆控制台指令

```bash
psql -U [user] -d [database] -h [host] -p [port]
```

-U 指定用户，-d 指定数据库，-h 指定服务器，-p 指定端口

完整的登录命令，比如使用 postgres 用户登录

```bash
psql -U postgres -d postgres
```

## 常用控制台指令

```bash
\password：设置当前登录用户的密码
\h：查看 SQL 命令的解释，比如\h select
\?：查看 psql 命令列表
\l：列出所有数据库
\c [database_name]：连接其他数据库
\d：列出当前数据库的所有表格
\d [table_name]：列出某一张表格的结构
\du：列出所有用户
\e：打开文本编辑器
\conninfo：列出当前数据库和连接的信息
\password [user]: 修改用户密码
\q：退出
```

## 允许远程访问

Mac下默认的postgresql目录的存放路径是`/usr/local/var/postgres/`，修改如下两个文件

* postgresql.conf
```config
listen_addresses = '*' #修改这里的配置允许任意地址的连接
```

* pg_hba.conf
```config
host all all 0.0.0.0/0 trust #配置服务端允许认证的方式
```

修改完成后重启

```bash
brew services restart postgresql
```
