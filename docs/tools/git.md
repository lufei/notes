## 修改最后一次提交的commit信息

```shell
git commit --amend
```

## 撤销上一次的commit

```shell
git reset HEAD~
```

## 修改remote url

* 直接修改
```shell
git remote set-url origin git@github.com:UserName/Repository.git
```

* 先删后加
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

!> 注意配置文件内的 127.0.0.1:1086 需要和本地 SS 客户端的所暴露的 本地 Socks5 监听地址 和 本地 Socks5 监听端口 一致

## Webhook

使用Swoole的HttpServer来作为Web服务，执行Github的Webhook

```php
<?php

define("SECRET", "test666");
define("PROJECT_PATH", dirname(__FILE__));

$http = new Swoole\Http\Server("0.0.0.0", 9501, SWOOLE_BASE);
$http->set(
    [
        'worker_num' => 1,
        'daemonize' => 1,
        'log_file' => PROJECT_PATH . '/swoole.log'
    ]
);

$http->on('workerStart', function ($server, $workerId) {
    cli_set_process_title("auto-pull" . "#{$workerId}");
});

$http->on('request', function ($request, $response) {
    $signature = $request->header['x-hub-signature'] ?? '';
    if (!$signature) {
        $response->status(404);
        return $response->end();
    }

    $json = $request->rawContent();
    $content = json_decode($json, true);

    list($algo, $hash) = explode('=', $signature, 2);

    //计算签名
    $payloadHash = hash_hmac($algo, $json, SECRET);

    // 判断签名是否匹配
    if ($hash === $payloadHash) {
        $cmd = "cd ".  PROJECT_PATH . " && git pull";
        $res = co::exec($cmd);
        $res_log = '[' . date('Y-m-d H:i:s') . '] [success] ';
        $res_log .= $content['head_commit']['author']['name'] . ' pushed ' . count($content['commits']) . ' commits' . PHP_EOL;
        $res_log .= $res["output"] . PHP_EOL;
        echo $res_log;
        return $response->end("success");
    }
    $res_log = '[' . date('Y-m-d H:i:s') . '] [error] secret error' . PHP_EOL;
    echo $res_log;
    $response->end("error");
});
$http->start();
```

## 压缩/合并commit

```shell
git rebase -i HEAD~<number>

# example : git rebase -i HEAD~4
# HEAD～4的含义是从头部开始追溯4条记录
```

执行后进入编辑模式，将需要压缩的commit前面的`pick`改为`squash`

```shell
# 取消
git rebase --abort

# 因为冲突打断的话 执行continue
git rebase --continue

# 强推
git push -f origin branch_name
```