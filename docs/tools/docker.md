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