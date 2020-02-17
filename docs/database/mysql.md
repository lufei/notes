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
