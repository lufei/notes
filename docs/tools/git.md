## 修改最后一次提交的commit信息

```shell
git commit --amend
```

## 修改remote url

```shell
git remote rm origin
git remote add origin git@github.com:UserName/Repository.git
```

## 同时推送多个平台

```shell
#github
git remote add origin git@github.com:UserName/Repository.git

#码云
git remote set-url --add origin git@gitee.com:UserName/Repository.git

#其他同理...
```

## 回滚上次push的提交

```bash
git reset --hard HEAD^
git add .
git commit
#强推
git push -f origin master
```

## 保持fork之后的项目和上游同步

```bash
#添加上游仓库
git remote add upstream [upstream_url]

#fetch
git fetch upstream

#将upstream/master merge到本地master分支
git merge upstream/master

#同时别忘了push到自己的github仓库
git push origin master
```

## 合并某个commitId

```bash
git cherry-pick commitId
```

## 22 to 443
git的ssh使用22端口不可用时，可以使用443端口
```bash
vim ~/.ssh/config

#写入
Host github.com
  Hostname ssh.github.com
  Port 443
```

## 设置SS代理

```bash
vim ~/.ssh/config

#写入
Host github.com
   HostName github.com
   User git
   ProxyCommand nc -v -x 127.0.0.1:1086 %h %p
```

!> 注意配置文件内的 127.0.0.1:1086 需要与您本地 SS 客户端的所暴露的 本地 Socks5 监听地址 和 本地 Socks5 监听端口 一致。