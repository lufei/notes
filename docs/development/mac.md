brew 工具参照 [Homebrew](tools/brew.md) 进行安装。

## PHP72

安装 PHP72 来代替系统自带的 PHP。

```shell
brew install php@7.2
brew link php@7.2 --force
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

## 编译 Swoole

创建一个`make.sh`文件，写入以下内容，注意替换对应的库路径

```shell
#!/bin/sh -e
__DIR__=$(cd "$(dirname "$0")";pwd)

cd ${__DIR__}
phpize --clean
phpize
./configure --enable-openssl --with-openssl-dir=/usr/local/opt/openssl  --enable-sockets --enable-mysqlnd --enable-http2
make clean
make -j
make install
```