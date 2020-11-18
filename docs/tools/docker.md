# Docker

## 删除所有容器

```shell
docker stop $(docker ps -qa)
docker rm $(docker ps -qa)
```

## 删除所有镜像

```shell
docker rmi --force $(docker images -q)
```

## Docker CE 镜像

```shell
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

https://developer.aliyun.com/article/110806

## 通过docker overlay2目录名查找容器名和容器ID

```shell
docker ps -q | xargs docker inspect --format '{{.State.Pid}}, {{.Id}}, {{.Name}}, {{.GraphDriver.Data.WorkDir}}' | grep "xxxxxxxx"
```
