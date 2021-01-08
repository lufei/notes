# Tools

## jq

用于命令行解析json数据，[文档](https://stedolan.github.io/jq/manual/)

### 获取 Swoole Release 版本

```bash
curl -s https://api.github.com/repos/swoole/swoole-src/releases/latest | jq '.tag_name' -r
```

### 获取 tag

```bash
curl -s https://api.github.com/repos/swoole/swoole-src/tags | jq ".[].name" -r | grep v4.5 | head -1
```