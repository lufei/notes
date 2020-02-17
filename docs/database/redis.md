## 命令行批量删除匹配到的key

```
redis-cli keys "*" | xargs redis-cli del
```