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

#切换到本地master分支
git checkout master

#将upstream/master merge到本地master分支
git merge upstream/master

#同时别忘了push到自己的github仓库
git push origin master
```

## 合并某个commitId

```bash
git cherry-pick commitId
```