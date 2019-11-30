WP-CLI 可以在不使用 WordPress 后台的情况下，仅通过命令行就可以完成 WordPress、主题、插件的安装、升级、使用等等

## 安装 WP-CLI

```bash
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
php wp-cli.phar --info # 检查是否可用
chmod +x wp-cli.phar
sudo mv wp-cli.phar /usr/local/bin/wp # 简化命令
```

## 安装 WordPress
```bash
wp core download
```

## 更新 WordPress 核心

!> 需要在 WordPress 项目的根目录下执行；如果使用 root 账户进行安装，需要我们新建一个新账户，如果不想新建可在命令后加上 `--allow-root`

```bash
wp core update --allow-root
```

?> 遇到 `429 Too Many Requests` 的时候，可以把源码通过 `wget` 下载后跟在命令后面进行更新

## 更新 WordPress 数据库

```bash
wp core update-db --allow-root
```