# Linux

## 修改主机名

```bash
hostnamectl set-hostname
```

退出 ssh 重新登录后生效

## 查看对应网卡流量

### 安装
```bash
yum install iftop

apt-get install iftop
```

### 使用
```shell
iftop -i eth0
```

## 修改ssh端口

```shell
vim /etc/ssh/sshd_config

#修改port后重启
service sshd restart
```

## 查看命令是否存在

```shell
if nonce=$(type php-config 2>&1) ;then
  echo "exist"
else
  echo "not exist"
  exit $?
fi
```

## Ubuntu 连接wifi

```bash
suto apt install net-tools wireless-tools network-manager

nmcli dev wifi connect "" password ""
```
