## 批量删除表查询语句

```bash
Select CONCAT( 'drop table `', table_name, '`;' ) FROM information_schema.tables Where table_name LIKE 'ram_%';
```