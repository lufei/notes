# Python

## Linux环境下安装Python3

```shell
mkdir -p /usr/local/python3
cd /usr/local/python3

wget https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tgz
tar -zxvf Python-3.6.1.tgz
cd Python-3.6.1
./configure --prefix=/usr/local/python3
make
make install

# 软链接 环境变量
ln -s /usr/local/python3/bin/python3 /usr/bin/python3
vim ~/.bash_profile
export PATH=$PATH:$HOME/bin:/usr/local/python3/bin
```