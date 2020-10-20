# MySQL

## 批量删除表查询语句

```bash
Select CONCAT( 'drop table `', table_name, '`;' ) FROM information_schema.tables Where table_name LIKE 'ram_%';
```

## IP存储

mysql存储ip，支持ipv4和ipv6。

```
varbinary(16)
```

```php
// 写入前：
inet_pton('127.0.0.1');
// 读出后：
inet_ntop($data['ip']);
```

## 远程访问

设置root账号可以远程连接

```sql
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;

flush privileges;
```

### 查看已有的iptables规则

在iptables规则里有一行是DROP，末尾以3306结尾的，在lnmp1.x里面序号是6，不同版本可能会不一样，自行确认

```shell script
iptables -L -n --line-numbers

iptables -D INPUT 6
```