# Mac

brew 工具参照 [Homebrew](https://brew.sh/) 进行安装。

## PHP

安装 PHP72 来代替系统自带的 PHP。

```shell
brew install php@7.2
brew link php@7.2 --force
```

```shell
brew install php@7.3
brew link php@7.3 --force

brew install php@7.4
brew link php@7.4 --force
```

## Composer

```shell
brew install composer
```

## MySQL

```shell
#先安装一下 cmake
brew install cmake

#安装 MySQL
brew install mysql@5.7

#添加环境变量
echo 'export PATH="/usr/local/opt/mysql@5.7/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc

#启动 MySQL
brew services start mysql@5.7

#初始化 MySQL，设置密码相关的
mysql_secure_installation
```

## MyCli

MySQL 的自动补全和语法高亮工具。

```shell
brew install mycli
```

## Redis

```shell
brew install redis

#启动 Redis
brew services start redis
```

## 修改 hosts

```shell
sudo vim /etc/hosts
```

## Core Dump

```shell
sudo mkdir /cores 
sudo chown root:admin /cores 
sudo chmod 1775 /cores
sudo chmod o+w /cores

ulimit -c unlimited

lldb -c /cores/core.37676
```

## TouchBar

音量和亮度调节消失

```bash
killall ControlStrip
```

## Nginx

```shell
brew install nginx
```
